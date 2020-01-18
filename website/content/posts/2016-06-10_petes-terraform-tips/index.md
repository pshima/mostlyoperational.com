---
title: "Pete’s Terraform Tips"
author: "Pete Shima"
date: 2016-06-10T18:20:12.367Z
lastmod: 2020-01-18T11:48:57-08:00

description: ""

subtitle: "My Terraform experience started with a single Terraform environment which is over a year old in production with over 3000 Terraform applies…"
tags:
 - AWS
 - DevOps
 - Terraform
 - Hashicorp
 - Infrastructure As Code




aliases:
    - "/petes-terraform-tips-694a3c4c5169"

---

My Terraform experience started with a single Terraform environment which is over a year old in production with over 3000 Terraform applies and over 4500 versions of state. The single environment grew to multiple environments; staging, an improved production, and environments built to run inside customer sites.

While none of these environments are large scale, they are somewhat diverse spanning multiple cloud providers. Given the age of the configuration and changes in Terraform over time there may be some learnings here that will help others.

Disclosure: I work for HashiCorp. Terraform is free and open source software. Upcoming Terraform features and changes are likely to change these tips and this post was written based on Terraform 0.6.16.

### Preface

This post is not intended for first time Terraform users but some of the advice may be interesting for beginners.

This does not talk about a popular topic among Terraform which is how you build your make files and scripts, organize your repositories and manage your state with Terraform. This is all managed for me [automagically](https://atlas.hashicorp.com) and is not something I have had to worry about.

### Get a naming scheme for your Terraform variables

This sounds like an obvious one not specific to Terraform, but it is really important when you start referencing variables that are dynamically created within your Terraform runs or from your module outputs that you have consistent, intuitive naming. The Terraform graph can get complex and sometimes it can be difficult to determine exactly what went wrong. Having spent a considerable amount of time just chasing down typos or name changes in variables, a solid naming scheme for variables and outputs will help save you time.

A good rule of thumb is that the variable you pass in to a module should mirror the variable name you are passing in as the value. Note the below which has an example of a direct variable and a module definition. Note how they differ, but the end variable is the same. The larger your Terraform environment the more headaches this is likely to avoid.
`module “vpc-peering” {  
 source             = “../../terraform/shared/network/vpc-peering”  
 vpc_peering_id     = “${var.vpc_peering_id}”  
 vpc_peering_cidr   = “${var.vpc_peering_cidr}”  
 az1_route_table_id = “${module.routing-private.az1_route_table_id}”  
 az2_route_table_id = “${module.routing-private.az2_route_table_id}”  
 az3_route_table_id = “${module.routing-private.az3_route_table_id}”  
}`

### Understand Terraform state

Terraform does a great job of abstracting it’s state management from you but **understanding in detail what state is and how to manipulate state will help you when you get stuck**. Make a new Terraform testing environment with a few resources, open the state file. Remove a resource, look at the state again.

It’s also important to know that if your Terraform apply fails, any modified resources will be applied to the state. It is not a big bang state change, each modified resource will get applied to the state even if the overall apply fails.

You’ll also notice at the top of the state file a serial. This is an incrementally increasing number with each state changes. If you make changes to the state manually you need to increase this sequencer.
`{  
    &#34;version&#34;: 1,  
    &#34;serial&#34;: 2348,`

The `terraform remote` command can be used to configure and push and pull remote state: [https://www.terraform.io/docs/commands/remote.html](https://www.terraform.io/docs/commands/remote.html)

### Careful with interpolation

I see a lot of people trying to simplify their configuration by using Terraform [interpolation](https://www.terraform.io/docs/configuration/interpolation.html), but sometimes this can have the opposite effect of adding complexity where you don’t need it. Honestly, just be explicit in your configuration and don’t follow the DRY principle like it’s going out of style. If you have 2 resources of something, that probably aren’t changing often, forget about trying to make it magical with interpolation functions, just repeat the configuration. I see a lot of configuration where lists or maps are defined as variables and then interpolation is used across the repository.

A common example of this is something like the below in the terraform.tfvars file:
`azs = “us-east-1b,us-east-1c,us-east-1d”`

And then the use of it something like this to pull an AZ based on the count of a resource
`az = “${element(split(“,”, var.azs), count.index)}”`

But what happens when you need to add or remove an availability zone? In this configuration every single resource using your var.subnet_ids is going to be modified or recreated when you change update this variable to add a new availability zone. For base level resources like subnets it is likely these are used over a vast majority of your configuration.

A different pattern is to not use a list
`az1 = “us-east-1b”  
az2 = “us-east-1c”  
az3 = “us-east-1d”`

And when passing the variable in to your module, specify the variables individually, this allows you to have a configuration that doesn’t want to recreate large portions of your stack or cause a big refactor. In this case adding a new AZ is done safely a module definition at a time, rather than a big bang. In some cases this will allow you to remove the interpolation altogether making a more human understandable and readable config.
`azs = “${var.az1},${var.az2},${var.az3}”`

This isn’t a plea to stop using interpolation, in fact Terraform interpolation is awesome, it’s just a reminder to think about how you use it. Is the interpolation helping you save time writing your config or is it causing you confusion each time you change your modules? Stop using counts for resources that rarely change in size.

Upcoming Terraform features are likely to make this only easier and better.

### Use modules

This doesn’t mean just use modules when you need to duplicate something. **Your main.tf file should contain only variable definitions, modules definitions, outputs and that’s it.** Your main.tf file should be your environment specific configuration that sets your environment specific variables and the modules you need for that environment.

Make a separate directory to hold you modules or use remote modules through GitHub. An advantage to using remote modules is you can also select state in time modules at specific revision. This can allow you to update a module and use different revisions across different environments.
`source = “github.com/hashicorp/vault//terraform/aws?ref=v0.5.0”`

### Avoid nesting modules

Nesting modules is appealing because you can effectively create collections of modules and pass in a single set of variables.
`main.tf  
 -&gt; moduleCollectionA  
   -&gt; moduleNetwork  
   -&gt; moduleStorage  
   -&gt; moduleCompute`

The disadvantage here is in the increased amount of work needed to make changes. In the example above if you need to remove something from moduleStorage, you now have to make the change in 3 places. Changing the variables and config in moduleStorage, changing the variables, config and outputs in moduleCollectionA, and changing the variables and config in main.tf.

At first this doesn’t seem like much additional work but in larger refactors when you need to make 20+ changes in this way it is easy to make mistakes. Terraform plan is there to save the day but I find it is easier to just avoid the double nesting when possible and use directory structures to organize code instead of nested modules.

### Output basic resource outputs in modules and use the default names

This is somewhat similar to the naming standards listed above, but is slightly more specific. Majority of Terraform resources have outputs when they are created. In the example of an [AWS EC2 instance](https://www.terraform.io/docs/providers/aws/r/instance.html) this has outputs like the instance id, IP address and DNS name among other details.

When writing module definitions it’s appealing to only output the variables you need. In the EC2 instance case maybe I only needed the IP address of the machine, and I added this as an output. I would recommend adding all the main variable outputs you think you might use when creating these modules and to use the exact same output name as Terraform uses. It generally takes a lot less time to add the rest of the basic outputs for a resource than it does to update it later when you need it, and using the same name really simplifies things.

Again in the [EC2 instance example](https://www.terraform.io/docs/providers/aws/r/instance.html) the instance id is exported as “id”.

It can be common to want to set this output to “instance_id”, but in reality to remember what name you chose when you wrote the module requires you tracing back through the configuration to hunt for this variable name. Instead, consider using the same exact outputs as the Terraform references docs and just using those as your main reference.
`output “id” { value = “${aws_instance.main.id}” }`

Your module definition will take care of the naming for you automatically, prefixing it with your module definitions name as well meaning you wont have a bunch of the same “id” variables floating around, but a single one, already prefixed with the exact resources you wanted.

### Targeted applies and taints

Terraform taint and targeted Terraform applies are great tools for your Terraform tool belt that you should get familiar with.

[Terraform taint](https://www.terraform.io/docs/commands/taint.html) is a command that allows you to mark a resource for recreation. For example if someone logged in to an instance and made some manual changes you can simply run a “terraform taint name.of.resource” and terraform will automatically destroy and create this resource.

Targeted applies are making changes to single terraform resources at a time. I have found this to be most handy during debugging or troubleshooting stages. In the case where some manual changes were temporarily required using a cli or console, you can easily reset these single resources with targeted applies. Terraform plan also works with targeted applies so this can help in using it in regular workflows and double checking changes.

Both of these tools require the name of the resource to be specified, a solid naming scheme here helps!

### Use module outputs to help shape the Terraform graph

Sometimes you want to have more control over the ordering of resources, but you don’t want to use targeted applies to control this. [Depends on](https://www.terraform.io/docs/configuration/resources.html#depends_on) can also help but sometimes there are cases where neither of these are exactly what you want. It can also be tricky to use depends on in module definitions.

In those cases you can use a simple trick to link things together. If you use the output of one module as the input of another, Terraform will automatically figure out this dependency, :boom:.

### Summary

I hope these Terraform tips were useful to you. If they were, please leave a comment or you can [tweet at me](https://twitter.com/Petey5K).
