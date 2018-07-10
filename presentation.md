## How to build _**250**_ single page applications with _AWS Lambdas_

^ Hi Everybody, I'm really happy to be here

---

# Who Am I ?

NAME: _Max_ [^1]

SURNAME: *Gallo*

TWITTER: *@_maxgallo*

SPECS: *Biped*, *Pasta eater*, *Work at* DAZN, *JavaScript developer*, *mediocre iOS Developer*, *Functional & Reactive programming learner*

[^1]: or Massimiliano if you like Italian spelling challenges

^ Italian Spelling Challenge

---

## Why am I talking in the _AWS User Group UK_ ?

---

Because since March I’ve been working with *AWS Lambdas*, *S3* and *DDB* 

# to create the *DAZN 2.0* <br/>_**Front End**_ build pipeline.

^ Front End

---

## What I'm going to _**talk**_ about

- Introduction to *DAZN*
- Why we needed a *Build Pipeline*
- How it works
- Takeaways

^ Important understanding the product

---

![right fit](images/dazn.jpg)

# [fit]  *DAZN*
## The Netflix of Sport

![inline 30%](images/dazn_new_logo_white.png)

- Monthly subscription
- All Sports Included
- Available on any device

^ Launched Aug 2016

^ For DAZN pronunciation, I suggested "EA Sports" Man

---


# _DAZN_ **2.0**

### Multiple _**Single Page Applications**_,
### tailored per country and device

^ Minimum amount of code / assets

^ Payments method example


---

# HOW MANY *SPA* ARE WE TALKING ABOUT?

| HOW MANY | WHAT | Seriously, WHAT? |
| --- | --- | --- |
| *1* | *Application* | dazn.com |
| *5* | *Countries* | JP, DE, CA, CH, AT |
| *5* | *Chapters* | catalog, auth, help, … |
| *10* | *Targets* | Web, Mobile, Android Tv, Xbox, Amazon Firestick, …|

We _**just**_ need to build 5 * 5 * 10 = *250 SPA*

---

# What we want to achieve

<br />

- Easy to *maintain* and *adopt*
- *Not always on* - It's a build system after all
- *Infrastructure as code*

---

<br />
# [fit] Welcome to: _**The Tube**_

![inline 200%](pdf/tube.pdf)

^ Stations

^ "Mind the PR" Slack Channel

---

# [fit] Moving in the _**Tube**_
# *Functional* & *Reactive*

 - Each [^2] *Station* is an *AWS Lambda*
 - Each *Station* is Stateless and Atomic
 - Each *Station* is triggered by event reaction


![right fit](pdf/fromto0.pdf)

[^2]: almost each

---

# From _**Code**_ to _**Test & Static Analysis**_
![inline 150%](pdf/step1.pdf)

---

# Inside _**Code**_

<br/>

- One repo per *Target*
- Each *Target Repo* contains all the chapters
- GitHub webhook to a Lambda functions to trigger the next step

---

# Inside _**Test & Static Analysis**_

Custom implementation, using *Docker Swarm* and *Bash*
 
1. Checkout target project from GitHub
- Run Unit Tests
- Run Static Analysis
- Compress everything and store on S3

---

# From _**Test & Static Analysis**_ to _**Prepare**_
![inline 150%](pdf/step2.pdf)

---

# Inside _**Prepare**_
<br />

1. Download the project code from S3
- Magic [^3]
- Pack everything and re-upload to S3

[^3]: You have to trust me on this one

---

# From _**Prepare**_ to _**Build**_
![inline 150%](pdf/step3.pdf)

---

# Inside _**Build**_ *Lambda*
 
### It builds the project code, without knowing *how* to build it.
 
1. Download the project code from S3
- Read configurations from the project code
- Build the project
- Pack the build output files and upload to S3

---

# From _**Build**_ to _**Optimise**_
![inline 150%](pdf/step4.pdf)

---


# Inside _**Optimise**_ *Lambda*
 
### Optimise the build output.
 
1. Download the build output files from S3
- Optimise JavaScript files
- Optimise Html and CSS as well.
- Pack the optimised files and upload them to S3
- This code is now ready to be used

---

# From _**Optimise**_ to _**Upload**_
![inline 150%](pdf/step5.pdf)

---

# Inside _**Upload**_ *Lambda*
 
### Upload the build output.

1. Download the optimised build output files from S3
- Upload the code to Artifactory
- Update Database about new available build

---

# Putting all together
![inline ](pdf/tube_icons.pdf) 

---

# Wait !

What about the *250 Single Page Applications* ?

![inline](gif/batman.gif)
 
---

Truth is, that the _**Tube**_ is more like this

![inline](pdf/multi-tube.pdf)

--- 

![right fit](pdf/fromto_multi.pdf) 

<br />

# _**Prepare**_ is actually a *Multiplier*

- It saves multiple files on S3
- Multiple events generated
- Multiple lambdas triggered

---

### Instead of *one pipeline*
# We now have *250* of them!

![inline](gif/mind_blow.gif)

---

# Takeaways

### *Organisational* & *Technical*

---

# *#* Organisational

- Easy learning curve
- *+ Devs* - Ops
- Relatively *low costs*
- You can use different Cloud Vendors

^ Growing team

^ Almost free tier

---

# *#* Tech

- Frameworks & Language agnostic
- Bounded Context
- Reactive Flow

^ Builder doesn't know how to build 
^ Atomic Build Output
^ No Orchestration

---


# [fit] Thanks

twitter: *@_maxgallo*
slides: *[github.com/maxgallo/lambdas-in-dazn](https://github.com/maxgallo/lambdas-in-dazn)*
medium: *[https://medium.com/dazn-tech](https://medium.com/dazn-tech)*



