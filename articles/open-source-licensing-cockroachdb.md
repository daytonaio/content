---
title: "Navigating Open Source Licensing: Lessons from CockroachDB's Recent Changes"
description: "An in-depth look at the recent licensing changes by Cockroach Labs and what they mean for startup CEOs relying on open-source software."
date: 2024-08-19
author: "Viaksh Prem Sharma"
---

# Navigating Open Source Licensing: Lessons from CockroachDB's Recent Changes

## Introduction

Cockroach Labs, the original developer behind the distributed SQL database CockroachDB, has announced a major change to its licensing model. The new system ensures that businesses only pay for things they really need. In particular, customers with annual revenues over $10 million now have to pay by the number of CPUs or CPU cores in their server system In contrast, startups and small businesses who annual revenue below of $10 million may continue to use the enterprise version for free.

Understanding these changes is important for startup CEOs. The updated licensing policy directly impacts how your business can use CockroachDB, especially if your company is in the development phase. This article explores CockroachDB license changes, what they mean for your business, and the processes for managing such changes in an open-source software environment

### TL;DR

- **Cockroach Labs Licensing Update**: CockroachDB's new licensing model now requires companies with over $10 million in annual revenue to pay for its usage.
- **Impact on Startups**: Smaller companies and individual developers can still use CockroachDB's enterprise features for free, but there are implications for scalability and cost as businesses grow.
- **Key Takeaways**: Startup CEOs must stay informed about licensing terms, understand the business models behind OSS, and plan for potential changes in their tech stack.

## The Shift in CockroachDB's Licensing

Cockroach Labs, the company behind CockroachDB, has recently made a significant change to its licensing model. Starting with version 24.3 on Nov. 18, the company will consolidate its self-hosted product under a single enterprise license, a move designed to ensure that larger companies contribute financially for using their software.

### Key Changes:

- **New Licensing Model**: The new CockroachDB Enterprise License (CEL) requires any company with more than $10 million in annual revenue to pay based on the number of CPUs or CPU cores used.
- **Support for Startups**: Smaller companies, individual developers, students, and academic researchers can continue to use the enterprise features for free, maintaining the accessibility that has made CockroachDB popular among startups.
- **Retirement of Core Offering**: The free Core offering will be retired, replaced by a streamlined 30-day trial experience for the enterprise tier, giving all users access to the full capabilities of CockroachDB.

This licensing change is aimed at preventing larger businesses from using the software for free while still supporting smaller startups. Cockroach Labs' goal is to sustain its business model while continuing to innovate and support the open-source community.

## Why This Matters to Startup CEOs

`Is it possible to consider how CockroachDB’s licensing changes affect the lives and businesses of startup CEOs?` Startups usually prefer open-source software because it allows them to obtain robust technology without spending money on expensive proprietary options. Yet, this move made by CockroachDB also showcases a risk that comes with relying on OSS.

### Key Considerations:

- **Scalability and Costs**: As your startup scales, what begins as a free tool can become a significant expense if your business grows and falls under the new licensing terms.
- **Licensing Awareness**: The CockroachDB example underscores the importance of understanding the motivations behind open-source projects and the potential for licensing changes.
- **Contribution to OSS**: Startups may need to consider contributing financially to the OSS projects they depend on, not just to support those projects but to ensure their continued availability.

## Future of Open Source

As all these license changes accumulate, it may be tempting to believe that open source is dead. `is it really?`

See the matter isn’t quite so simple, Most of the software world is permeated with open source components, including CockroachDB itself, which relies on many third-party libraries, languages and toolkits and it's own internal technology [Pebble key-value store](https://github.com/cockroachdb/pebble) is also and open source.

So, `open source is far from dead`, but its foundation is becoming increasingly uncertain—especially when it comes to commercial, vendor-driven projects, as recent developments over the past five years have shown.

## Conclusion

Recent changes to CockroachDB’s licensing model are a reminder of the growth of open-source software. As a startup CEO, it’s important to understand the importance of understanding and planning for this change. Open-source software can provide great benefits, but it also comes with its own set of risks and responsibilities.

By keeping you informed, conducting due diligence, and being proactive in managing your software stack, you can ensure that your startup stays agile and ready for any changes that come your way and by doing so so you're not only protecting your business but you're protecting wider open source - also contributing to the community, ensuring that these valuable resources continue to thrive.

## References

- [Cockroach Labs Enterprise License Announcement](https://www.cockroachlabs.com/blog/enterprise-license-announcement/)
- [Peter Zaitsev's Twitter Discussion on Licensing](https://x.com/PeterZaitsev/status/1824088154795802642)
- [TechCrunch Article on Cockroach Labs' Licensing Change](https://techcrunch.com/2024/08/15/cockroach-labs-shakes-up-its-licensing-to-force-bigger-companies-to-pay/)
- [Hacker News Discussion on CockroachDB Licensing](https://news.ycombinator.com/item?id=41256222)

- [SiliconANGLE: Cockroach Labs changes](https://siliconangle.com/2024/08/15/cockroach-labs-changes-self-hosting-license-single-enterprise-model/)
