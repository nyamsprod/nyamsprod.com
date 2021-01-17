---
title: "Why I never implemented PSR-12"
date: "2020-11-10"
categories: 
  - "humeurs"
tags: 
  - "oop"
  - "php"
  - "php-fig"
  - "psr"
---

Last week I finally decided to update most of my OSS to get them ready for PHP8. In doing so I locked my repo to github since [travis is about to drop open source CI/CD integration](https://www.jeffgeerling.com/blog/2020/travis-cis-new-pricing-plan-threw-wrench-my-open-source-works "https://www.jeffgeerling.com/blog/2020/travis-cis-new-pricing-plan-threw-wrench-my-open-source-works") and I took the time to update static analysis tools but when it came to my coding style rules, I did nothing. Yes I left it as it has always been. My current set of rules are based on PSR-2 with a superset of rules that I like. I did not even bother to check if the code was still in line with the replacing PSR, which is PSR-12 and I will try to tell you why.

Back in the days when PSR-1 and PSR-2 was voted on their was a huge adoption rates. The reason was simple it was backed by all the major frameworks at that time and even despite the space vs tab controversy there was not so much discussion. The contentious rules where either dropped, added in the separate PSR-2 recommendation or left to the discretion of users.

Fast forward to PSR-12 which superseded PSR-2 by fixing some of its bugs/oversights and added new rules. The people behind PSR-12 did a great job. Some may disagree on some of the new rules but having followed how the recommendation came to be accepted, the authors deserve a lot of respect and consideration. Having said that, in my mind, they made 2 big mistakes that made me come to the conclusion that I should not care about PSR-12.

The first mistake was that in opposition to PSR-2 which was build on experiences, statistic usage in all main frameworks using older recommendation as basis (PEAR, Zend coding style to name but a few), PSR-12 was build on assumption meaning that some rules where created while the feature were not already available, PSR-12 was build to go along with PHP7 (I am oversimplifying here). Either way, people were not given proper time to really assess if the rule was exactly how people would end up using the new syntax.

The second mistake is the PSR acceptance flow. By the time PSR-12 was accepted, PHP, the project, had already announced/implemented/discussed new syntaxes for PHP8 making PSR-12 dead on arrival as it was certified with never tested practices and was already outdated because new syntaxes were not taken into account. Yet, it was still advertised as covering new features which makes the whole exercise miss its target or ambition. Furthermore, the current workflow means that to add all those new PHP syntaxes, like how to properly style the [new match expression](https://wiki.php.net/rfc/match_expression_v2 "https://wiki.php.net/rfc/match_expression_v2") or [attributes](https://wiki.php.net/rfc/shorter_attribute_syntax "https://wiki.php.net/rfc/shorter_attribute_syntax"), we need a brand new PSR to replace PSR-12. In the meantime, those syntaxes are not covered by any PSR, so frameworks, library maintainers and users are left choosing whatever they prefer. Which ultimately will lead to going back to a pre-PSR world where everyone will practically do whatever he/she thinks is the correct way of writing those new syntaxes.

Thankfully we don't need to go that far back. We now have mature tools to enforce coding style on project. Tools like [php-cs-fixer](https://cs.symfony.com/ "https://cs.symfony.com/") can be hooked to your CI/CD pipeline and supports PSR-2/PSR-12 rules as basis but are not limited to them. Those tools can also be easily extended to support new rules as new syntaxes and features are added to the language. Last but not least they can evolve faster than the current recommendations.

Having said that, we still need some kind of common ground just for the sake of readability between projects. And while I'm not a fan of every recommendation in PSR-12, PSR recommendations are still the de-facto based coding standard for the PHP community. So a way forward should be to make PSR regarding coding style evolve faster and a good way to do it would be to make them rely on **a living standard** document just like the WHATWG group did for HTML.  
Also it would be an added benefit to associate CS tools maintainers to that process so we as a community can benefit from their experiences and together build better rules and improve PHP coding style rules just like PHPStan/Psalm are driving user-land static analysis forward currently.

Whatever process is chosen do keep in mind that projects will always add specific rules based on their usage/experience. The goal has never been to strictly follow any guideline but to use them as a foundation and adapt them to our codebase accordingly.
