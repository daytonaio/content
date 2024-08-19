# Daytona Content Programme for Technical Writers

Welcome to the [Daytona](https://www.daytona.io) `content` repository! This repo is dedicated to managing external technical writers who contribute articles and guides. Here, you'll find details on how to participate, contribute, and get compensated for your work.

## Table of Contents
- [Daytona Content Programme for Technical Writers](#daytona-content-programme-for-technical-writers)
  - [Table of Contents](#table-of-contents)
  - [Introduction](#introduction)
  - [Writing Guidelines](#writing-guidelines)
    - [Content Types](#content-types)
    - [Writing Structure](#writing-structure)
    - [Assets](#assets)
    - [Fact Checking](#fact-checking)
    - [Interlinking](#interlinking)
    - [Glossary/Definitions](#glossarydefinitions)
    - [Evergreen Content](#evergreen-content)
  - [Contribution Process](#contribution-process)
    - [Editing Process](#editing-process)
    - [Publication](#publication)
  - [Quality Assurance](#quality-assurance)
  - [Licensing and Copyright](#licensing-and-copyright)
    - [Payment](#payment)
  - [Contact and Support](#contact-and-support)

## Introduction
The `content` repository is a platform where technical writers can contribute articles to the [Daytona Dotfiles Insider](https://www.daytona.io/dotfiles/) blog by "solving" posted issues (proposed article ideas) through pull requests. Merged PRs are eligible for compensation.

## Writing Guidelines

### Content Types
- **Articles**: In-depth explorations of topics, at least 800 words.
- **Guides**: Step-by-step instructions for specific tasks or processes, at least 1500 words.

### Writing Structure
- Use the provided templates in `articles` and `guides` folders.
- Follow the naming convention: `YYYYMMDD_title_of_the_content.md`.
- Structure content with H2 subtitles for easy navigation.
- Include a comprehensive introduction before the first H2 section.
- Utilize formatting techniques: **bold**, *italic*, `code elements`, and links.
- Incorporate notes, quotes, TL;DR sections, and key points for enhanced readability.

### Assets
- Store images in the `/assets` folder within the respective content type folder.
- Name images consistently: `YYYYMMDD_title_of_the_content_img1.png`.
- Reference images using relative paths from the `/assets` folder.

### Fact Checking
Ensure all information is accurate and up-to-date. Verify facts and cite sources where necessary.

### Interlinking
Link relevant keywords to:
- [Daytona Dotfiles Sitemap](https://www.daytona.io/sitemap-dotfiles.xml)
- [Daytona Definitions Sitemap](https://www.daytona.io/sitemap-definitions.xml)

### Glossary/Definitions
Mark new terms that could be added to the Daytona Definitions page with a comment containing a concise description.

### Evergreen Content
Focus on creating long-lasting content. Avoid referencing specific versions of technology that may quickly become outdated.

## Contribution Process

1. Choose an open [issue](https://github.com/daytonaio/content/issues) (proposed article idea).
2. Fork the repository and create a new branch for your content.
3. Write your article or guide following the provided templates and guidelines.
4. Submit a pull request for review.

### Editing Process
- Articles undergo up to two rounds of editing.
- Use tools like [Grammarly](https://grammarly.com), [Hemingway App](https://hemingwayapp.com/) and [LanguageTool](https://languagetool.org/) for initial proofreading.
- Respond promptly to editorial feedback and make necessary revisions.

### Publication
Upon approval, you'll be informed of the publication date.

## Quality Assurance
We use `markdownlint` to ensure consistency in Markdown formatting. Run `npm run lint` before submitting your PR to check for any style issues.

## Licensing and Copyright

By contributing to this repository, you agree that all content you submit is subject to the following terms:

1. **Copyright Assignment**: You assign all rights, title, and interest in and to the copyright of your contributed content to Daytona.

2. **Exclusive Rights**: Daytona retains exclusive, worldwide, royalty-free, perpetual, and irrevocable rights to use, reproduce, modify, adapt, publish, distribute, and display the contributed content in any form or medium.

3. **No Reuse Without Permission**: Contributors may not reuse, republish, or redistribute the content they've submitted without explicit written permission from Daytona.

4. **Attribution**: While Daytona owns the copyright, we will provide attribution to contributors as the original authors of the content, unless requested otherwise.

5. **Warranty**: By submitting content, you warrant that you have the right to assign copyright as described above and that the content does not infringe upon the rights of any third party.

These terms ensure that Daytona can freely use and manage the contributed content while acknowledging the valuable work of our contributors.

### Payment
- Compensation is provided for accepted and published content.
- Payment can be made directly or through bounties (if assigned to the issue).
- Payment can also be made directly if you can submit an invoice including:
  - Date, Title of Article/Guide, Amount
  - Payment details (Bank Name, Account Number/IBAN, Routing Number/SWIFT Code/ABA)
  - Address invoice to: Daytona Platforms Inc., 224 W 35th St Ste 500#297, New York, NY 10001, USA

## Contact and Support
- For questions or assistance, open an issue or contact the repo maintainers.
- Join our [Slack community](https://go.daytona.io/slack) for discussions and support.

Happy writing, and thank you for contributing to the Daytona Dotfiles Insider blog!
