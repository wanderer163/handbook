# Batch Changes strategy

Batch Changes is a tool to find code that needs to be changed and change it at scale by running code. This page outlines the vision, strategy, and goals of the Batch Changes team.

#### Quick links

- [Code Graph overall strategy](../../../../engineering/code-graph/batch-changes/index.md)
- [Batch Changes team page](../../../../engineering/code-graph/batch-changes)
- [Planning board](https://github.com/orgs/sourcegraph/projects/216)
- [Demo video](https://www.youtube.com/watch?v=eOmiyXIWTCw)
- [Batch Changes documentation](https://docs.sourcegraph.com/batch_changes)

# Vision

#### 1-year vision

Enterprise developers can easily run code to create changesets across many repositories and codehosts, and track them to completion.

We are focusing on enterprises first because the intensity of the pain increases with the size and age of a codebase, and with the number of teams working on it. Enterprises tend to be the places where those conditions exist and the need is the most intense. That allows us to be adopted fast, learn fast, and solve the most valuable problems for users that operate in a very large codebase. Some enterprises also have existing tooling that we can replace, serving as a validation that we are moving in the right direction.

#### 3-year vision

Bring the same experience to all developers.

Once we have created a product that is a leader for enterprises, we will focus on making it available to the largest number of developers possible.

#### 10-year vision

Automated code changes are a common practice for all developers.

Making that happen requires two layers. First, making it easy to run code to create changesets across many repositories and codehosts, provided you know how to write code that changes code. We will have achieved this with our 3-year vision. Second, writing code that changes code, or more generally making describing code changes easier. To deliver our 10-year vision, we will create interfaces that makes it easy to describe code changes and create an experience that makes it as intuitive to change code on the entire codebase as in an IDE.

## Mission & Strategy

### Mission

We allow developers to focus on changing their code, without having to do any plumbing (building scripts to interact with codehosts and integrate with other tools and workflow). We help them drive changesets to completion without having to rely on spreadsheets and painful coordination. Later on, we want to make it easier to write and run code that changes code.

### Strategy

To deliver our vision, we will:

- First, get adopted by the Sourcegraph customer base, including large enterprises. We will target customers with advanced practices and workflow, and collaborate with them to build a category-defining product that all other companies will use. This is what we are doing today.
- Concurrently, spread usage (MAUs) within our customer base, and make sure we deliver on our success metric (changesets merged).
- Then, create low time-to-value entry points into Batch Changes, and allow users unfamiliar with the practice of automating code changes to onboard with a smooth learning curve. Make onboarding Batch Changes self-serve for most users, to help our customers be successful and prepare for launching on Cloud.
- Then, release Batch Changes on Sourcegraph Cloud, and test and learn how we can serve individuals and smaller teams.
- Eventually, address the problem end to end by becoming the go-to place for code change tools and recipes.

# Guiding Principles

## Themes

To deliver the strategy, here are the themes we want to focus on for the next 3 years.

### Enterprise scale

We have the overarching goal to [level up our enterprise-ready features](../index.md#level-up-our-enterprise-ready-features). Batch Changes is successfully adopted by very large companies, with 10,000s of repositories. While there is no technical limitation for Batch Changes to run at that scale, there are 2 limitations in practice:

- Creating changesets locally takes too long to be practical for very large-scale changes.
- In companies with 10,000s of repositories, it is difficult for batch changes maintainers to understand what repositories they should target with a change, and to analyse the progress of a batch change.

To drive enterprise success and stickiness, we need to:

- Deliver a great experience in creating changesets at enterprise scale (10,000s repositories), resulting in more users onboarding batch changes.
- Make sure that iterating on batch changes has the lowest cycle time possible, and that the debugging experience is smooth.
- Allow users to find out where to create batch changes and understand what to do to get changesets merged in batch changes with 1,000s of changesets. This will increase the number of changesets merged, our key [success metric](../../../../engineering/code-graph/batch-changes/metrics.md).

### Discovery, configuration and onboarding

As we go to market, our install base of customers with Batch Changes enabled is growing. Often, a few teams have adopted Batch Changes in a given company, because they were the ones feeling the need at the time. That team is frequently used to making large-scale code changes and building automation, so adopting Batch Changes is easier for them and they later turn into evangelists inside the company. In order to go beyond that beachhead user base within a company, we want to make Batch Changes more discoverable, and self-serve for new users, both as a way to drive adoption within customers and increase value and stickiness, but also to prepare for the self-serve model of Batch Changes on Sourcegraph Cloud. We plan to:

- Make Batch Changes more discoverable within Sourcegraph.
- Provide pathways from Search into Batch Changes.
- Make onboarding self-serve and provide easy ways to get started.

### Adoption through low time-to-value usage patterns

The main use case for Batch Changes today is to automate creating changesets at scale, then track them to completion. This requires some time investment from users to get familiar with Batch Changes, and also to write the code required to automate code changes. This is great for the platform engineer persona or users that feel the urgency to adopt, but it does not allow for less committed users to discover Batch Changes and form habits.

We have heard from customers that tracking and managing changesets created _outside_ of batch changes is very valuable as it replaces manual tasks: track the status of changes across many teams and make sure they get merged. We think there is an opportunity to offer a low time-to-value entry point into Batch Changes by allowing users to import changesets easily, and use the tracking and management functions.

We also think we can deliver our vision by offering a way to change code across repositories, without writing code, and directly from the Sourcegraph navigation UI.

We plan to drive usage (MAUs) by implementing low time-to-value, high-frequency use cases.

### Cloud

We plan to achieve feature parity on Sourcegraph Cloud, including Batch Changes. There are two prerequisites for Batch Changes on Sourcegraph Cloud to be successful:

- Reducing time to value. Sourcegraph Cloud's user base will be primarily individual and commercial customers, at least at the beginning. Today, the value of Batch Changes increases exponentially with the size of a customer's codebase and team. Most customers with a smaller team and codebase do not face a big enough pain to invest the time and effort required to adopt Batch Changes in its present state. To be successful on Sourcegraph Cloud we need to make the time to value of Batch Changes shorter and drive [Adoption through low time-to-value usage patterns](#adoption-through-low-time-to-value-usage-patterns).
- Improving [Discovery, configuration and onboarding](#discovery-configuration-and-onboarding).

### Automate common code changes

The most frequent question that our customers ask when onboarding Batch Changes is "how do I write code to change x". Writing code to change code is not trivial, and although there are existing tools, most of them fall short either in usability or in expressivity. Having a way to find or write code that automates the change they want is the first critical step in our customer's job to be done, and is a prerequisite for automation.
By solving that problem, we will:

- Solve for our customer's job to be done (JTBD) end to end.
- Position ourselves to address competition specialized in one use case or language.
- Create defensibility by allowing users to share their code in a registry.

This last step is on the critical path for achieving our 10-year vision, but might not be necessary to achieve our 3-year vision.

# Where we are now

Batch Changes has just proved market fit and is adopted by a dozen customers. We see early adoption across a diverse set of companies, from public technology companies to startups with a few dozen engineers ([Batch Changes dashboard](https://sourcegraph.looker.com/dashboards-next/174)).

Over the first year, we have discovered a repeatable playbook: a platform engineering team, sometimes supported by a developer experience team, adopts Batch Changes to make large-scale code changes. Most of the use cases are relatively simple code changes, such as updating configuration files across many repositories. Some are more complex, such as changing API call sites to ship a breaking change in an internal library. The common denominator is those changes would take a very long time to create and track to completion using a manual approach. Adopting Batch Changes allows the platform team to automate manual work and save time, as well as transition from a model in which they are asking their customer teams to do some work, to a more proactive where they can propose a change themselves and leave customer teams to review and merge.

We have five main learnings from the first year of Batch Changes:

- The key success metric for customers is the number of changesets opened by Batch Changes that eventually get merged. To be successful, we need to increase adoption, and the merge rate of changesets.
- We have discovered that importing, tracking and managing existing changesets that were not created by Batch Changes, is perceived as very useful by customers. However, importing changesets today is clumsy, so this workflow is not very frequently used. We need to improve it and validate the value of this use case. If successful, it could create a low-friction, low time-to-value entry point into Batch Changes for new users and increase usage frequency and stickiness.
- Batch changes works great for teams with 1,000s of repositories, but gets clumsy to use for companies with 10,000s repositories.
- The job to be done (JTBD) for our customers is changing code at a large-scale. To do so, they need to automate a code change, apply it, then track it to completion. Batch Changes today is addressing applying and tracking changes, but the first thing many customers ask is "how do I write code that makes change x". To solve for our customers JTBD, we will need to provide an answer to that question.
- As users get more sophisticated and work on large, more complex batch changes, debugging and iteration cycle time become the bottlenecks.

# What's next and why

### Top customer, support, sales, and marketing issues

Customers tend to struggle with configuring Batch Changes. This delays trials, can create a bad first impression, and requires work from CEs and CSEs. The top issues surfaced to CSE, CE and Product are:

- Changesets are not syncing frequently enough. There also are many feature requests for a bulk sync operation ([#21458](https://github.com/sourcegraph/sourcegraph/issues/21548)), that indicate that users think changesets do not sync properly. The current root cause is that users haven't set up [webhooks](https://docs.sourcegraph.com/batch_changes/references/requirements#batch-changes-effect-on-code-host-rate-limits).
- Users struggle to configure credentials, and get confused by the various options (code host token, global service account, personal access token).

Besides configuration, there are lots of requests for [mounting files on batch change steps containers](https://github.com/sourcegraph/sourcegraph/issues/14851).

## FY 2022 Q4 goals

### Top priority: server side Batch Changes

This quarter, our main goal is to iterate on the [Experimental](https://docs.sourcegraph.com/admin/beta_and_experimental_features) release of [Server-side Batch Changes](https://github.com/sourcegraph/sourcegraph/issues/21018) (SSBC), and to onboard three early customers into a POC. We are focusing hard on SSBC because:

- It is essential for Batch Changes to work at [Enterprise scale](#enterprise-scale), and Enterprise customers with 10,000s of repositories have a degraded experience today, because they cannot create batch changes with 1,000s of changesets or resource-intensive batch changes in a reasonable amount of time. Server-side Batch Changes will directly impact key customers and prospects such as [1](https://github.com/sourcegraph/customers/issues/1), [2](https://github.com/sourcegraph/customers/issues/3), [3](https://github.com/sourcegraph/customers/issues/2) and [4](https://github.com/sourcegraph/customers/issues/6).
- It will shift the setup burden from the user to the site-admin. Once site-admins have setup SSBC, any user can run a batch change from the GUI in a few clicks. That will unlock improvements to [Discovery, onboarding and onboarding](#discovery-configuration-and-onboarding) such as creating batch changes from a template directly from the GUI instead of having a "cold start". Creating a guided, self-serve onboarding is a prerequisite for [Cloud](#cloud).
- It unlocks [key vision items](https://docs.google.com/document/d/1MnfaA9P7mtur7aQbMvy2x96_zy_IrOhY-MbGUo5I5wk/edit#heading=h.25ypvomeex1g) that will make using Sourcegraph an incredible experience and delight our customers, as well as [low time-to-value usage patterns](#adoption-through-low-time-to-value-usage-patterns).

We will iterate as we learn, but our focus will be on:

- SSBC reliably works at the scale of 1,000s of changesets.
- Users get a great editing experience, including a few basic templates.
- Users get a great debugging experience.
- Admins are able to setup SSBC in a reasonable amount of time.
- Admins can manage (monitor, view queue, etc) executors.

### Other priorities

After SSBC, this is our ordered list of priorities:

1. Build a minimal version of fork support ([#17879](https://github.com/sourcegraph/sourcegraph/issues/17879)). Users in companies with many changesets tend to run into write-permission issues when creating batch changes. This can be solved by creating forks. Besides, the permission model of [#565](https://github.com/sourcegraph/accounts/issues/565), [#544](https://github.com/sourcegraph/accounts/issues/544) and [#4778](https://github.com/sourcegraph/accounts/issues/4778) and likely other similar large scale customers, requires forks. Forks are necessary along with SSBC to allow large customers to create very large batch changes.
1. Tackle the top configuration issues encountered by customers:
   1. Nudge users to setup webhooks ([#24310](https://github.com/sourcegraph/sourcegraph/issues/24310)).
   1. Simplify credential management. We plan to remove using the codehost token for Batch Changes ([#25394](https://github.com/sourcegraph/sourcegraph/issues/25394)) that we deprecated in 3.29, and change the docs and in-product wording to clarify credential usage.
1. Iterate on [bulk actions](https://github.com/orgs/sourcegraph/projects/119?card_filter_query=label%3Abulk-action), to move it from a minimal experience to something that customers love. We lack bandwidth to make radical improvements, but we plan to ship small increments, as well as start tracking bulk action metrics ([#23882](https://github.com/sourcegraph/sourcegraph/issues/23882)).
1. (Rolled over from Q3) We are planning to allow users to [Mount file on batch change steps containers](https://github.com/sourcegraph/sourcegraph/issues/14851) after many customer requests.
1. Handle permission errors more gracefully (likely with [#24999](https://github.com/sourcegraph/sourcegraph/issues/24999s) and maybe with [#24307](https://github.com/sourcegraph/sourcegraph/issues/24307)). As we onboard larger customers, including on SSBC, permission errors are increasingly frequent, causing large batch changes to fail after hours of execution.
1. **Experiment:** We assume that if we provide low time-to-value entry points into the product, users will get into Batch Changes and some will become long-term users. This will increase the value batch change creates, and increase stickiness. We want to start testing this assumption as it may take several test and learn cycles to get to the final experience that works. We may timebox a small experiment like this if we are able to deliver on our other priorities.

### What we are not working on

- **Windows support** (#24849): Reliably supporting creating batch changes locally in a windows environment is a very large amount of work, that is incompatible with our plan of delivering Server-side Batch Changes as fast as possible. Windows support has blocked one [prospect](https://github.com/sourcegraph/customers/issues/3) and slowed down adoption at a [customer](https://github.com/sourcegraph/customers/issues/2), and will likely be important in the Banking and Gaming industry. We plan to address these customers with Server-side Batch Changes. Server-side Batch Changes will bypass the need to run the CLI locally, and instead allow customers to compute the batch changes on the Sourcegraph instance.

- **Adding a permission model**: Batch Changes currently only supports the site-admin and user roles. While finer-grained permissions will likely be needed to reach broad adoption in large companies, we are prioritizing building a product that supports [Enterprise scale](#enterprise-scale) before adding to the permission model. When Server-side Batch Changes is in beta and the user experience at a very large-scale allows for broad adoption, we can reconsider adding more complex permissions and control over who uses Batch Changes.

- **Bitbucket Cloud**: Batch Changes currently supports Bitbucket Server, but not Bitbucket Cloud. We plan to add Bitbucket Cloud ([#24199](https://github.com/sourcegraph/sourcegraph/issues/24199)) in the future as it would increase our addressable market and is requested by some customers and prospects. We are not prioritizing it this quarter, because we focus on making Batch Changes great at [Enterprise scale](#enterprise-scale) before increasing our addressable market.

- **Education material about code change tools:** Helping our customers find and select a code change tool that suits their needs is a very common ask, and something we think could drive adoption. We don’t have bandwidth for this this quarter though.

- **Integrating with other features**: In the future, we want Batch Changes to fit in an integrated Sourcegraph experience. A code insights could include a batch change to track and fix a bad code pattern. Code monitoring could be used to trigger batch changes. The code graph could be used to change code across repositories. SSBC tends to be a prerequisite for this type of experiences, as they require triggering and executing a batch change. We intend to focus more on building that unified experience once SSBC is in Beta and has a small user base.
