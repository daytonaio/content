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
    - [How To Contribute](#how-to-contribute)
    - [Editing Process](#editing-process)
    - [Code Contributions](#code-contributions)
    - [Quality Assurance](#quality-assurance)
    - [First Time Contributor](#first-time-contributor)
    - [Parallel Submissions](#parallel-submissions)
    - [Publication](#publication)
  - [How to Propose a New Content](#how-to-propose-a-new-content)
  - [Licensing and Copyright](#licensing-and-copyright)
  - [Payment](#payment)
  - [Contact and Support](#contact-and-support)
  - [Showcase Your Contributions](#showcase-your-contributions)
    - [Available Awards](#available-awards)
    - [Top Contributors](#top-contributors)


## Introduction
The `content` repository is a platform where technical writers can contribute articles to the [Daytona Dotfiles Insider](https://www.daytona.io/dotfiles/) blog by "solving" posted issues (proposed article ideas) through pull requests. Merged PRs are eligible for compensation.

> **Note:** Always use GitHub as the main communication channel. For questions not directly related to the project or for general clarifications, join the designated `content` channel on the Daytona Community Slack.

## Writing Guidelines

### Content Types
- **Articles**: 1000-2000 words. In-depth topic exploration with expert quotes, statistics, and subheadings. Informative yet conversational tone.
- **Guides**: 1500-3000 words. Step-by-step instructions with screenshots, troubleshooting tips, and materials checklist. Clear, concise language.
- **News**: 500 words. Concise and fluent updates focusing on the 5 W's and H (Who, What, Where, When, Why, and How).
- **Ghostwriting:** Variable length. Content written in another's voice, matching their style, tone, and expertise.

### Writing Structure
- Use the provided templates in `articles` and `guides` folders.
- Follow the naming convention: `YYYYMMDD_title_of_the_content.md`.
- Structure content with H2 subtitles for easy navigation.
- Include a comprehensive introduction before the first H2 section.
- Utilize formatting techniques: **bold**, *italic*, `code elements`, and links.
- Incorporate notes, quotes, TL;DR sections, and key points for enhanced readability.

### Assets
- Every article should include at least one image or illustration. If you are using someone else's work, please ensure you have permission to do so (copyright) and properly credit the author. You can utilize tools like Excalidraw and Tldraw to create basic illustrations of concepts. While the logic is crucial, aesthetics can be refined later by a designer.
- Store images in the `/assets` folder within the respective content type folder.
- Name images consistently: `YYYYMMDD_title_of_the_content_img1.png`.
- Reference images using relative paths from the `/assets` folder using Markdown `![Alt text for the image](URL_to_image)`.
- If any comparisons or quantifiable work are included, they should be presented in tables formatted in Markdown.

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

### How To Contribute

1. Choose an open [issue](https://github.com/daytonaio/content/issues) (proposed article idea).
2. Fork the repository and create a new branch for your content.
3. Write your article or guide following the provided templates and guidelines.
4. Submit a pull request for review and use the name of the article for the title.
5. If multiple PRs are submitted by different individuals, we will typically prioritize those that demonstrate the clearest and most well-crafted writing.

### Editing Process
- If the PR meets our standards, the issue will be assigned to you, and the editing process will commence.
- Articles undergo up to two rounds of editing.
- Use tools like [Grammarly](https://grammarly.com), [Hemingway App](https://hemingwayapp.com/) and [LanguageTool](https://languagetool.org/) for initial proofreading.
- Respond promptly to editorial feedback and make necessary revisions.

### Code Contributions

If your article includes code examples or projects, please follow these steps:

1. **Create a New Repository**:
   - Create a new public repository on your GitHub account.
   - Name it appropriately, related to the article's topic.

2. **Add Code to the Repository**:
   - Upload all relevant code, scripts, or project files to this new repository.
   - Ensure the repository includes a README with clear instructions on how to use or run the code.

3. **Link the Repository in Your Article**:
   - In your article, include a link to this new repository.
   - Example: "The complete code for this project can be found in `[this GitHub repository](link-to-your-repo)`."

4. **Maintain the Repository**:
   - Keep the repository updated with any changes or improvements mentioned in your article.
   - Respond to issues or pull requests from readers who might have questions or suggestions.

5. **License**:
   - Include an appropriate open-source license in your repository to clarify how others can use or contribute to your code.

By following these steps, you ensure that readers have access to the full code examples and can easily follow along with your article. It also provides a way for the community to engage with your work and potentially contribute improvements.

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

### Parallel Submissions

To ensure fairness and efficiency in our content creation process, we have implemented the following policy regarding parallel submissions:

- An individual author may only have one active attempt (PR) at a time.
- Parallel attempts on several issues from the same author will not be considered until the first attempt is cleared.
- Once an author's initial submission is cleared (either approved or not), they may then proceed to work on another issue.

This policy helps us maintain a balanced workload among contributors and ensures that each submission receives the necessary attention and review. It also allows us to provide timely feedback and support to authors throughout the content creation process.

We encourage authors to focus on producing high-quality content for one issue at a time, rather than attempting to work on multiple submissions simultaneously. This approach typically results in better-crafted articles and a more streamlined review process.

### Publication
Upon approval, you'll be informed of the publication date.


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
- Payment can be made through Algora as bounties (if assigned to the issue and your PR gets merged).


## Contact and Support
- For questions or assistance, open an issue or contact the repo maintainers.
- Join `#content` channel in our [Slack community](https://go.daytona.io/slack) for discussions and support.

Happy writing, and thank you for contributing to the Daytona Dotfiles Insider blog!

## Showcase Your Contributions

Highlight your contributions to this repository and display your achievements with pride!

To see all badge holders for this repo, check out the [Vaunt.dev community board](https://community.vaunt.dev/board/daytonaio/repository/content).

You can add your own achievements to your profile or README by using the following code snippet:

```html
<p>
  <img src="https://api.vaunt.dev/v1/github/entities/YOUR_GITHUB_USERNAME/achievements?format=svg&limit=3" width="350" />
</p>
```

Make sure to replace `YOUR_GITHUB_USERNAME` with your actual GitHub username.

We encourage all contributors to proudly display their achievements and inspire others to get involved!

Your contributions, big or small, are valued and recognized.

### Available Awards

| Name | Icon | Description |
| ---- | ---- | ----------- |
| Tech Scribe | <img src="https://raw.githubusercontent.com/daytonaio/content/main/.vaunt/tech_scribe.png" width="150" /> | Penned first Daytona Dotfiles Insider article |
| Parable Crafter | <img src="https://raw.githubusercontent.com/daytonaio/content/main/.vaunt/parable_crafter.png" width="150" /> | 5 Daytona tales of tech insight! Your wisdom grows! |
| Koan Master | <img src="https://raw.githubusercontent.com/daytonaio/content/main/.vaunt/koan_master.png" width="150" /> | 10+ Daytona articles! A fount of profound tech wisdom! |
| Ummon's Disciple | <img src="https://raw.githubusercontent.com/daytonaio/content/main/.vaunt/ummons_disciple.png" width="150" /> | Unmerged PRs spark thought like Ummon's cryptic teachings! |
| Cosmic Observer | <img src="https://raw.githubusercontent.com/daytonaio/content/main/.vaunt/cosmic_observer.png" width="150" /> | Stargazing the Daytona cosmos! Your journey awakens! |
| Quantum Proposer | <img src="https://raw.githubusercontent.com/daytonaio/content/main/.vaunt/quantum_proposer.png" width="150" /> | Idea proposed! Daytona multiverse feels your ripples! |


### Top Contributors
<p>
  <img src="https://api.vaunt.dev/v1/github/entities/daytonaio/repositories/content/contributors?format=svg&limit=10" width="600" />
</p>