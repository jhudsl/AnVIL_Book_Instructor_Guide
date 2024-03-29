


This book is targeted towards people who are teaching a course or workshop on AnVIL. You will find here:

<br> <!-- Capital letter makes part of below content indented which doesn't look good.. can remove the <br> if more text is added above -->
<br>

- **Overview** -- Design philosophy and goals for this guide - is this a good fit for your class?  What should you know before you start?
- **Account Setup** -- Step-by-step instructions to create your first accounts on AnVIL and create your first class Workspace
- **Developing Content** -- Additional tools to help you customize your class Workspace
- **Class Setup** -- Step-by-step instructions to help you add students into a class on AnVIL
- **Class Ending** -- Best practices for finishing your course cleanly and minimizing costs
- **Student Account Setup** -- Step-by-step account set up for students using AnVIL in your class

## Why should I use AnVIL?

You may be wondering if AnVIL is a good choice for your class. We feel the answer is an unequivocal YES. One of the greatest strength of AnVIL is that it provides [version control](https://git-scm.com/book/en/v2/Getting-Started-About-Version-Control) of the program being used, so that you the instructor no longer have to devote time to solving issues caused by students using multiple operating systems or installing different versions of a program onto their computer. This also prevents unexpected run errors and limits the amount of troubleshooting you have to do. As a result, classes and activities will run more smoothly and predictably, allowing for an easier time with scheduling. Additionally, using AnVIL means that all students can participate in the activity without needing to provide computers that have certain specifications. Finally, AnVIL gives your students low-stress and low-stakes experience working with cloud-computing platforms, which is becoming common in today's bioinformatics workplaces.

## Goals for This Guide

<img src="resources/images/02_Overview_files/figure-html//1HHWg47Tg6miv_K7GNB6ZDTx-4Jc5IMl7APfFtD1Rqag_ge21c626cf0_0_5.png" title="List of goals for this guide: (1) get your accounts, (2) set up billing, (3) create your first Workspace, (4) develop content, and (5) set up classes with students." alt="List of goals for this guide: (1) get your accounts, (2) set up billing, (3) create your first Workspace, (4) develop content, and (5) set up classes with students." width="480" />

## Design Philosophy

This guide provides an opinionated walkthrough on how to set up AnVIL for your class.  These step-by-step instructions take instructors that are completely new to the AnVIL through account setup to the point where you can feel comfortable hosting a class from start-to-finish on AnVIL. Following the recommendations in this guide will help you minimize expenses, develop content programmatically, track individual student expenses, and stop billing expenses from accruing once the class is complete. In support of these goals we have made the following design decisions:

1. ACCOUNT SETUP

a. Sign up for a personal Google Cloud Account, where you can get started by claiming [$300 free Google credits](https://cloud.google.com/free/docs/gcp-free-tier/#free-trial).

2. CONTENT DEVELOPING

a. Include version control and visibility of course content by using GitHub. This will allow you to add content programmatically, keep track of changes, and share your content with others outside of AnVIL.

3. CLASS SETUP

a. Create a separate Google Billing Account for each class. This will allow you to easily shut down expenses at the end of the class.
b. Choose one funding source per class (for example, the [STRIDES](#strides-funding) Program).
b. Create separate Terra Billing Projects for each student. This will allow you to monitor billing expenses closely and work with students to build best computing practices.

# Before You Start

- You will need a **credit card or bank account** to activate your free trial and get started. Don't worry! **You won't be billed until you explicitly turn on automatic billing**, but payment information is needed for verification purposes.
- Before setting up billing yourself, you may want to check with your institutional procurement office and see if they have a preferred account set-up method with Google (such as a third party reseller or an existing account).
- You can also work with your AnVIL collaborators or grant program officer to determine an appropriate Google Billing Account or Terra Billing Project for your class.
