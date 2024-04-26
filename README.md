# Kubernetes-win-11-home-gotchas
Windows 11 Home Gotchas when trying to run Minikube

I really enjoyed learning the fundamentals of Kubernetes and getting hands on, but to start with, things where not so easy. 

The main issues being my Windows 11 Home operating system. I ran into issues right from the work go when trying to start up Minikube.  I was getting warning messages and errors about not having VTX enabled. When I checked my bios all the settings seemed correct and my hardware (Dell G5 5000, Intel(R) Core(TM) i7-10700F, 16 gb RAM) supporting virtualisation.

Also Hyper-V, which is the default virtualisation driver on Windows does not work on the home edition.  It is only available in Pro, Enterprise and Education editions of Windows. You might see this error if you run **minikube start**

```
X Exiting due to PR_HYPERV_MODULE_NOT_INSTALLED: Failed to start host: creating host: create: precreate: Hyper-V PowerShell Module is not available

* Suggestion: Run: 'Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V-Tools-All -All'

* Documentation: https://www.altaro.com/hyper-v/install-hyper-v-powershell-module/

* Related issue: https://github.com/kubernetes/minikube/issues/9040Then I had random proxy related issues, where i could not access to external repos.
```

Using Virtualbox and the no VTX check would enable me to start Minikube

```
minikube start --driver=virtualbox —-no-vtx-check
```

There was also a warning Hyper-V being more efficent, you can safely ignore that.


Then I had random proxy related issues, where i could not access to external repos. 

```
! This VM is having trouble accessing https://registry.k8s.io
* To pull new external images, you may need to configure a proxy: https://minikube.sigs.k8s.io/docs/reference/networking/proxy/
```

When I did get this working, not quite sure how as I tried a lot of things (installing Docker Desktop, Installing and trying out PowerShell 7 as admin), I found Minikube to be really flaky. 
It would hang often and was chewing up memory.

Thankfully I have an old Linux mini PC lying around. After sourcing a new power cable I got this booted up with Linux Mint. Everything worked first time and like a charm, despite the box a lot older and with a less powerful CPU.

In all I lost a good few hours / days trying to get it working on my main Windows desktop. 

I would recommend spinning up a Linux VM on a cloud provider, if you do not happen to have a Linux box lieing around. Just be sure you pick on that supports virtualisation (Azure / AWS). 

TL DR;

Don’t bother trying to run Minikube on a Windows Home PC. Spin up a Linux instance instead. 

I hope someone finds this useful and it save you time. If you'd like to check out my finding of learning and researching Kubernetes then check out my blog post

https://www.cohezion.com.au/blog/kubernetes-k8-use-cases-pros-and-cons
