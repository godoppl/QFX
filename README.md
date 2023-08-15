# PROPOSAL: Quality Filtered 𝕏 (Twitter)

### ℚ𝔽𝕏
Pronounced: kfi·tuh

(Subject to change)


## The tl;dr

A proxy or a built in feature to 𝕏 where users, for a montly fee or using their own HW, can set a threshold on the objective quality of content they wish to consume.


## What we hope to achieve

An increase in quality of content on social media platforms, while refraining from the use of censorship.


## The general idea

An agent is trained on posts on the 𝕏 platform, with the objective to provide a "Quality Rating" (QR) on the post, on a scale from `0.0` to `1.0`.
The QR is an *objective* score of the quality of the content in the post. Informative and uplifting posts get a high QR. Shit-posting and personal attacks get a low QR.
The QR is not context-aware, so even if the post is meant to be tongue-in-cheek or sarcasm, it will receive the QR score as if it was posted in a vacuum.

[Training of the agent is explained here](#the-agent)

Subscribed users can adjust the minimum QR score for the content they wish to interact with. This is called the "threshold".
The threshold can be adjusted individually for non-followers, followers, users you follow, individual users, DMs and similar.

Users would get a "Quality Index" (QI), based on the quality of the content they provide to the platform.
Calculating the QI can be done using a simple median (ignoring outliers) of the QR score of the users past posts, or something more nuanced.
A cutoff for the past posts in question could be: The last 6mo. or 500 posts, whichever is lowest. This is to give users the chance to influence their QI in a resonable timeline.
Subscribed users can then use the QI to discern the quality of the users they wish to follow, or maybe even impose a threshold to whom can follow them.

The QI could also be influenced by the reporting behaviour of the user. If a user reports other users for breaking TOS, the user can receive an adjustment of QI based on the validity of that report.
This aims to deter users with a large following to attack users using their follower-base as a "mob", and rather use the appropriate action to deal with such users.


## Why this is not censorship

The idea here is not to censor users or what they are allowed to post, but to provide the ability for the end-user to impose a quality threshold on the content they wish to interact with.
This is very different from censorship because it upholds the freedom to post content of any kind (within legality and TOS), and whomever wishes to interact with said content is free to do so.

This must be able to resist any political, religious or ideoligical biases in the QR scoring by using properly processed training data.

[A propositon on how to achieve this](#the-agent)


## Defining quality

There will probably be many factors on which quality can be rated and discerned. We have not concluded what all those factors are, and would like for this to be an open discussion.

Some factors could be:
- The positivity/negativity of the content.
- Attacks on individuals, groups or entities.
- Informative content.
- Long-term factually correct content. (Recently established facts are more prone to being disproven)
- Content in violation of the TOS of the platform.
- ...

We suspect that the vast majority of content could be given a resonable QR on text content alone, and it is a great start to achieving what we want.

We understand that there are additional challenges when defining the QR of posts containing images or other media, these will probably be solved at some stage.
With regards to fact-checking, we might want to assign a separate agent for this purpose. This agent could feed into and adjust the QR, this will be another challenge.


---

## The agent

### Collecting, cleaning and preparing the training data

Having an objective way to assert the QR of a post starts with the training data.

Here is a proposed way to prepare this data:
1. Scrape a sample of posts from the platform or use an existing, suitable dataset.
2. Anonymize the posts. Only the content of the post is needed for the training. Remove any references to entities such as religions, companies or persons with neutral definitions.
3. Divide the posts into 2 ratings, "High quality" and "Low quality".
4. Compare 2 posts with an equivalent rating, and define one of the posts "better quality", "similar", "lower quality" than the other.
5. Repeat step 4 until the complete dataset has been run through.
6. Sort the dataset in order of quality, and distribute a decimal rating across all posts ranging from `1.0` on the high side, to `0.0` on the low side.
7. Pick 2 posts with a similar rating, not necessarily directly ajacent, and perform the same distinction from step 4. Adjusting the rating as needed.
8. Repeat step 7 until adjustments are not needed anymore, or the dataset is deemed sufficently rated.

At this point the dataset should be prepared.

The size of the dataset is dependant on the resources available, but more is usually better.
Some, or most of these steps can probably be done using an off-the-shelf LLM, even better, a fine-tuned one.
For using human classifiers, we would suggest using a diverse set of people, to dilute any bias that could be introduced.
Any bias that still persist, can be reduced further with reinforcement learning of the agent. [More on that here](#fitment-and-reinforcement).


### Defining the model

A suitable model has not been decided, and suggestions are welcome by using a PR or the Discussions feature of GitHub.
We believe that a model with a few million parameters or even less, should be capable of this task.

Models like [Twitter-roBERTa-base for Sentiment Analysis](https://huggingface.co/cardiffnlp/twitter-roberta-base-sentiment-latest) already exists, but can probably be improved upon.


### Fitment and reinforcement

The training of the model will probably require more resources than we currently have available, so we are open to offers for assisting with this.

Constant reinforcment learning is something we feel is necessary in order to weed out bias and to ensure we follow the cultural landscape.
Using RLHF with a diverse set of individuals, in tandem with LLM based RL, is probably a good way to achieve this.

A proposed way to get individuals to provide human feedback is to use the userbase that would be gathered with this platform. We suggest using either free months of membership or cashback as rewards for assisting in the RLHF loop.
Users with an upper-tier QI could be picked to participate, which should result in better feedback. However, other means of quality control are also necessary. Diversity of participants should always be of importance.

The dataset could be increased by picking new posts that have received a QR, and using a similar tactic to step 4 in the data preparation stage. The new data should be subjected to the same procedure as in step 2 of the data preparation stage.
It would probably be wise to not use posts that a user would have already seen on the platform for this purpose, since the user can have a predisposed bias by knowing the context.


---

## How do we implement this?

There are multiple ways, but each come with their challenges:
- Standalone app using the API from X via a proxy which filters the content for the user.
- Browser extension that handles this client-side on the X or X Pro websites.
- X implements this directly into their systems.
- Open source proxy software, which users can deploy the agent on their systems or networks to filter their own timeline.
- SaaS proxy which does the same as the former.


## Who is going to make this happen?

If you want to take this idea and run with it, go for it! We just want to see this happen.

If someone wants to make a startup and have us be a part of it, [email me](mailto:godoppl@gmail.com)

If you want to fund us to make this a reality ourselves, [email me](mailto:godoppl@gmail.com)

If you work at 𝕏 and want this to be part of the core experience, convince the management to [email me](mailto:godoppl@gmail.com)
