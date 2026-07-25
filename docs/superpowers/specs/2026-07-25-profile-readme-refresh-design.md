# Profile README Refresh Design

## Goal

Refresh Ilya Aghaei's GitHub profile README so it accurately presents his current front-end work, highlights live projects and portfolio, and keeps the existing red visual identity without the GitHub statistics section.

## Visual Direction

- Preserve the current red capsule-render header and footer.
- Keep the layout centered where visual elements benefit from it.
- Retain the Contribution Game / Pacman section unchanged.
- Use a cleaner hierarchy with fewer decorative separators and more purposeful badges.
- Apply the requested Bitcount Grid Double typeface through a GitHub-compatible rendered SVG element, because GitHub strips inline `<style>` tags and external CSS imports from README content.
- Keep native Markdown section headings for accessibility, maintainability, and reliable rendering.

## Content Structure

1. **Hero**
   - Keep the ILYA / XLIYA banner.
   - Present Ilya as a Front-End Developer focused on React, Next.js, and TypeScript.
   - Keep GitHub and location badges.
   - Remove the MRB Group / Company badge.
   - Add a prominent Portfolio badge linking to `https://ilya-aghaei-portfolio.vercel.app/`.
   - Update the animated or rendered headline to use Bitcount Grid Double where supported.

2. **Current Projects**
   - Feature both Asman and Wavify.
   - Link Asman to `https://asman-web.ir/`.
   - Link Wavify to `https://wavify.ir/`.
   - Use concise descriptions based on the resume:
     - Asman: dealership management platform with dashboards, customer management, parts-order tracking, surveys/analytics, and inventory workflows.
     - Wavify: Persian music streaming platform with discovery, recommendations, playlists, libraries, uploads, and chat.

3. **About Me**
   - Update the summary from the resume without exposing private contact details.
   - Mention 1+ year of professional experience.
   - Emphasize responsive production web apps, component-based UI architecture, state management, REST/WebSocket integration, and maintainable code.
   - Keep Karaj, Alborz as the location.

4. **Featured Projects**
   - Add a visually consistent live-project showcase for:
     - Wavify — `https://wavify.ir/`
     - Rudo Quest — `https://rudo-quest.vercel.app/`
     - Indigo Accessories — `https://indigo-accessories.vercel.app/`
     - Asman — `https://asman-web.ir/`
   - Use compact cards or a two-column table with project name, short description, and a clear live-site link.
   - Do not invent detailed product claims for Rudo Quest or Indigo Accessories when those details are not present in the supplied resume.

5. **Tech Stack and Tools**
   - Keep the existing icon-driven presentation.
   - Align the stack with the resume by including React, Next.js, TypeScript, JavaScript, Redux, Tailwind CSS, Material UI, Node.js, Git, Figma, Vercel, and Postman where supported.
   - Keep useful existing workflow tools without adding a company affiliation.

6. **GitHub Activity**
   - Remove the complete GitHub Stats section, including stats, top languages, streak, and trophy images.
   - Keep the Contribution Game / Pacman section.

7. **Footer**
   - Preserve the red capsule-render footer wave.

## Compatibility and Accessibility

- Use only markup and image services that render in GitHub profile READMEs.
- Do not include `<style>` or `@import`, because GitHub sanitizes them.
- Every image must have meaningful alt text.
- All external destinations must use HTTPS.
- Avoid personal phone number and email from the resume.
- Keep the README usable if third-party image services temporarily fail by retaining readable text headings and links.

## Verification

- Confirm the Company badge and GitHub Stats section are absent.
- Confirm all five requested destinations (four live projects plus portfolio) appear with correct URLs.
- Confirm Asman and Wavify both appear under Current Projects.
- Confirm the Pacman contribution graph remains present.
- Confirm HTML tags are balanced and Markdown structure is valid.
- Inspect the final diff to ensure no unrelated content or files are changed.
