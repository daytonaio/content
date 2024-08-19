<br>

<div align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://github.com/daytonaio/daytona/raw/main/assets/images/Daytona-logotype-white.png">
    <img alt="Daytona logo" src="https://github.com/daytonaio/daytona/raw/main/assets/images/Daytona-logotype-black.png" width="40%">
  </picture>
</div>

<br>

<div align="center">

[![Issues - Content](https://img.shields.io/github/issues/daytonaio/content)](https://github.com/daytonaio/content/issues)

</div>

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
    - [AI-Generated Content](#ai-generated-content)
  - [Contribution Process](#contribution-process)
    - [Editing Process](#editing-process)
    - [Publication](#publication)
    - [Quality Assurance](#quality-assurance)
    - [First Time Contributor](#first-time-contributor)
  - [How to Propose a New Content](#how-to-propose-a-new-content)
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
Each article should ideally contribute one new definition to the Daytona Definitions page. Please submit this in the designated directory for definitions, using the provided template. This falls within the scope of producing a content piece.

### Evergreen Content
Focus on creating long-lasting content. Avoid referencing specific versions of technology that may quickly become outdated.

### AI-Generated Content
We recognize the potential of AI-assisted writing tools. However, all content must meet our high standards for quality, readability, and originality:

- AI-generated content is acceptable if it's well-integrated, natural-sounding, and indistinguishable from human-written text.
- Avoid generic AI-generated phrases like "in the ever-growing age" or "in the dynamic world of..."
- Focus on clear, concise, and engaging writing, regardless of whether AI tools are used.
- All content will be evaluated based on its quality. Lazy or poorly written content will be rejected, whether AI-generated or not.
- Writers are responsible for fact-checking, editing, and refining any AI-generated content to ensure it meets our standards.

Remember, good writing is good writing, regardless of how it's produced. Our goal is to provide valuable, well-crafted content for our readers.


## Contribution Process

1. Choose an open [issue](https://github.com/daytonaio/content/issues) (proposed article idea).
2. Fork the repository and create a new branch for your content.
3. Write your article or guide following the provided templates and guidelines.
4. Submit a pull request for review.
5. In the event that multiple PRs are made from different people, we will generally accept those with the clearest writing.

### Editing Process
- If the PR meets our standards, the issue will be assigned, and the editing process will commence.
- Articles undergo up to two rounds of editing.
- Use tools like [Grammarly](https://grammarly.com), [Hemingway App](https://hemingwayapp.com/) and [LanguageTool](https://languagetool.org/) for initial proofreading.
- Respond promptly to editorial feedback and make necessary revisions.

### Publication
Upon approval, you'll be informed of the publication date.

### Quality Assurance
We use `markdownlint` to ensure consistency in Markdown formatting. Run `npm run lint` before submitting your PR to check for any style issues.

### First Time Contributor
If you're contributing to the Daytona Content Programme for the first time, we require you to create a short author profile. This profile will be used to credit you for your work and provide readers with information about your background and expertise. Follow these steps to create and submit your author profile:

1. Create a new Markdown file in the `authors` folder.
2. Name the file using the format `firstname-lastname.md` (e.g., `jane-doe.md`).
3. Use the provided template in the `authors` folder to fill out your profile information.
4. Fill in all the fields with your information.
5. Place your author image and company logos in the `authors/assets` folder, using clear and descriptive filenames.
6. In your profile, reference the image and logo files using relative paths from the `authors` folder.
7. Once you've completed your profile, include it in the same pull request as your first content contribution.

## How to Propose a New Content

We welcome new ideas and contributions from our community. If you have a suggestion for a new article or guide, or maybe a significant improvement of the existing content, here's how you can propose it:

1. **Check Existing Issues**: Before creating a new issue, please check the [existing issues](https://github.com/daytonaio/content/issues) and Daytona Dotfiles Insider blog to avoid duplicates.

2. **Create a New Issue**:
   - Go to the [Issues tab](https://github.com/daytonaio/content/issues) of this repository.
   - Click on the "New Issue" button.
   - Choose the "Content Production Request" issue template.

3. **Fill in the Details**:
   - Title: Provide a clear, concise title for your proposed article or guide.
   - Description: Include a brief overview of what the article should cover.
   - Please ensure that all other fields are filled out completely without omitting any.

4. **Add Labels**: Add relevant labels to your issue to help categorize it (e.g., "article", "guide", "enhancement").

5. **Submit the Issue**: Click "Submit new issue" to create your proposal.

6. **Engage in Discussion**: Once submitted, maintainers or other community members might comment on your issue. Be prepared to engage in constructive discussion to refine the proposal.

Remember, creating an issue is just the first step. If you're interested in writing the article yourself, please indicate this in your issue. Otherwise, another writer may pick up the topic.


## Licensing and Copyright

By contributing to this repository, you agree that all content you submit is subject to the following terms:

1. **Copyright Assignment**: You assign all rights, title, and interest in and to the copyright of your contributed content to Daytona.

2. **Exclusive Rights**: Daytona retains exclusive, worldwide, royalty-free, perpetual, and irrevocable rights to use, reproduce, modify, adapt, publish, distribute, and display the contributed content in any form or medium.

3. **No Reuse Without Permission**: Contributors may not reuse, republish, or redistribute the content they've submitted without explicit written permission from Daytona.

4. **Attribution**: While Daytona owns the copyright, we will provide attribution to contributors as the original authors of the content, unless requested otherwise.

5. **Warranty**: By submitting content, you warrant that you have the right to assign copyright as described above and that the content does not infringe upon the rights of any third party.

These terms ensure that Daytona can freely use and manage the contributed content while acknowledging the valuable work of our contributors.


## Payment
- Compensation is provided for accepted and published content.
- Payment can be made directly or through bounties (if assigned to the issue).
- Payment can also be made directly if you can submit an invoice including:
  - Date, Title of Article/Guide, Amount
  - Payment details (Bank Name, Account Number/IBAN, Routing Number/SWIFT Code/ABA)
  - Address invoice to: Daytona Platforms Inc., 224 W 35th St Ste 500#297, New York, NY 10001, USA


## Contact and Support
- For questions or assistance, open an issue or contact the repo maintainers.
- Join `#content` channel in our [Slack community](https://go.daytona.io/slack) for discussions and support.

Happy writing, and thank you for contributing to the Daytona Dotfiles Insider blog!
