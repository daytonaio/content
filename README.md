<div align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://github.com/daytonaio/daytona/raw/main/assets/images/Daytona-logotype-white.png">
    <img alt="Daytona logo" src="https://github.com/daytonaio/daytona/raw/main/assets/images/Daytona-logotype-black.png" width="40%">
  </picture>
</div>

<div align="center">

[![Issues - Content](https://img.shields.io/github/issues/daytonaio/content)](https://github.com/daytonaio/content/issues) [![Vaunt Community](https://api.vaunt.dev/v1/github/entities/daytonaio/repositories/content/badges/community)](https://community.vaunt.dev/board/daytonaio/repository/content)

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
  - [Showcase Your Contributions](#showcase-your-contributions)
    - [Top Contributors](#top-contributors)

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
By contributing to this repository, you agree that all content you submit is subject to the terms outlined in the [CONTRIBUTING.md](CONTRIBUTING.md) file.

## Payment
- Compensation is provided for accepted and published content.
- Payment can be made through Algora as bounties (if assigned to the issue and your PR gets merged).

## Contact and Support

<<<<<<< HEAD
- For questions or assistance, open an issue or contact the repo maintainers.
- Join `#content` channel in our [Slack community](https://go.daytona.io/slack)
  for discussions and support.

## Showcase Your Contributions

Along with the chance to earn bounties, each engagement comes with an
achievement badge.

Showcase your contributions in your GitHub profile and display your achievements
with pride! For more information, check the
[CONTRIBUTING.md](CONTRIBUTING.md#showcase-your-contributions) file.

### Top Contributors

<p>
  <img src="https://api.vaunt.dev/v1/github/entities/daytonaio/repositories/content/contributors?format=svg&limit=10" width="600" />
</p>

<<<<<<< HEAD
You can showcase your achievement badges on your GitHub profile in the following
way:

=======
<<<<<<< HEAD
<<<<<<< HEAD
Happy writing, and thank you for contributing to the Daytona Dotfiles Insider blog!
<<<<<<< HEAD
=======
You can showcase your achievement badges on your GitHub profile in the following way:
=======
You can showcase your achievement badges on your GitHub profile in the following
way:

>>>>>>> 3b409bd (fixed linting issues and changes some rules)
>>>>>>> 6a73653 (fixed linting issues and changes some rules)
<p>
  <img src="https://api.vaunt.dev/v1/github/entities/nkkko/achievements?format=svg&limit=3" width="400" />
</p>

Simply add the following code to your GitHub profile README file:

```html
<p>
  <img
    src="https://api.vaunt.dev/v1/github/entities/USERNAME/achievements?format=svg&limit=3"
    width="400"
  />
</p>
```

<<<<<<< HEAD
Happy writing, and thank you for contributing to the Daytona Dotfiles Insider
blog!
=======
<<<<<<< HEAD
Happy writing, and thank you for contributing to the Daytona Dotfiles Insider blog!
>>>>>>> de0091a (added example)
=======
Happy writing, and thank you for contributing to the Daytona Dotfiles Insider
blog!
>>>>>>> 3b409bd (fixed linting issues and changes some rules)
>>>>>>> 6a73653 (fixed linting issues and changes some rules)
=======

=======
>>>>>>> ecef784 (readme splitted into 3 files)
## Showcase Your Contributions
Along with the chance to earn bounties, each engagement comes with an achievement badge.

Showcase your contributions in your GitHub profile and display your achievements with pride! For more information, check the [CONTRIBUTING.md](CONTRIBUTING.md#showcase-your-contributions) file.

### Top Contributors
<p>
  <img src="https://api.vaunt.dev/v1/github/entities/daytonaio/repositories/content/contributors?format=svg&limit=10" width="600" />
</p>
<<<<<<< HEAD
>>>>>>> f2efc13 (added vaunt section)
=======

<<<<<<< HEAD
Happy writing, and thank you for contributing to the Daytona Dotfiles Insider blog!
>>>>>>> ecef784 (readme splitted into 3 files)
=======
You can showcase your achievement badges on your GitHub profile in the following way:
<p>
  <img src="https://api.vaunt.dev/v1/github/entities/nkkko/achievements?format=svg&limit=3" width="400" />
</p>

Simply add the following code to your GitHub profile README file:
```html
<p>
  <img src="https://api.vaunt.dev/v1/github/entities/USERNAME/achievements?format=svg&limit=3" width="400" />
</p>

```

Happy writing, and thank you for contributing to the Daytona Dotfiles Insider blog!
>>>>>>> de0091a (added example)
