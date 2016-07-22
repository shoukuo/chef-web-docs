---
title: 'Remediate compliance failures on your Ubuntu infrastructure with Chef'
layout: lesson-overview
platform: 'Ubuntu'
logo: ubuntu.svg
order: 2
---
In the previous tutorial, [Assess your infrastructure with Chef Compliance](/compliance-assess/ubuntu/), you set up a Chef Compliance server and scanned an Ubuntu 14.04 server against the predefined CIS Security Benchmarks.

We proposed these 5 stages for meeting your compliance challenges: **Analyze**, **Specify**, **Test**, **Remediate**, and **Certify**. In the previous tutorial, you covered the first 3 of these 5 stages.

The fourth stage is **Remediate**. Knowing the state of your servers is a great first step towards meeting your compliance goals. But how can you remediate compliance failures and ensure that the remediation _stays_ good?

With Chef, you write code to describe the desired state of your infrastructure. When Chef runs, it applies the configuration only when the current state differs from the desired state. This approach is called _test and repair_.

You can use Chef's test and repair approach to remediate compliance failures. A complete workflow might use an automated pipeline, such as [Chef Automate](https://www.chef.io/automate/). This diagram shows a more basic workflow that you can use to get started.

<img src="/assets/images/networks/compliance_workflow.svg" style="width: 100%; box-shadow: none;" />

**remediate locally**<br>The workflow begins with local remediation. In this step, you write Chef code, or _cookbooks_, on your workstation and apply that code to local test instances that resemble your production environment. Testing your code on local instances helps you to experiment and iterate more quickly.

**upload cookbooks**<br>After you verify that your cookbook remediates the compliance failure on a local test instance, you can upload it to the Chef server. Chef server acts as a central repository for your cookbooks and for information about your servers, or _nodes_.

**run chef-client**<br>[chef-client](https://docs.chef.io/chef_client.html) runs on a node. It downloads the latest cookbooks from Chef server and then applies them. You can set up `chef-client` to run on-demand, periodically, or in response to a change.

**scan & verify**<br>After `chef-client` runs on your node, you repeat your compliance scan to verify that the compliance failure was correctly remediated.

In this tutorial, you'll implement this workflow to resolve the failure to the **Ensure Firewall is active** rule you saw in the previous tutorial. You'll start by remediating the failure locally on a virtual machine. Then you'll upload your cookbooks to the Chef server, run `chef-client` on your node, and rescan your node.  

After completing this lesson, you should be able to:

* test the remediation on a local instance.
* update a node with the remediation.
* prove that the remediation fixed the compliance failure.

Let's get started by ensuring you're all set up.