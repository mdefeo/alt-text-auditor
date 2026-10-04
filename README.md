# Alt Text Auditor

Audit WordPress images for missing alt text and generate context-aware suggestions from metadata, filenames, and content.

> **Status:** Early development / portfolio project

## Overview

Alt Text Auditor is a lightweight WordPress plugin for identifying images with missing or incomplete alternative text and helping editors create better accessibility metadata.

Rather than simply flagging blank alt text, the plugin is designed to provide useful, reviewable suggestions based on information already available in WordPress, including:

- Attachment captions
- Attachment descriptions
- Attachment titles
- Cleaned image filenames
- Featured-image context
- Post and page titles
- Excerpts and surrounding content

The goal is to make alt-text cleanup faster without automatically replacing human judgment.

## Why This Plugin?

WordPress makes it easy to upload and reuse images, but alt text is often skipped, inconsistent, or added without enough context.

Alt Text Auditor is intended to help site owners and content teams:

- Find images that need review
- Understand where those images are used
- Generate sensible starting-point suggestions
- Review and approve changes before they are applied
- Avoid treating every blank alt attribute as an error

A blank alt attribute can be correct for a purely decorative image, so the plugin is designed around **auditing and human review**, not blind automation.

## Planned Features

### Audit Images

- Find Media Library images with missing alt text
- Display image thumbnails and attachment metadata
- Show filename, title, caption, and description
- Identify featured images
- Show where an image is used when possible
- Filter and sort audit results

### Context-Aware Suggestions

Generate suggested alt text using signals such as:

1. Attachment caption
2. Attachment description
3. Attachment title
4. Cleaned filename
5. Featured post/page title
6. Post excerpt
7. Surrounding content context

Suggestions may include metadata describing how they were generated, for example:

```php
[
    'text'       => 'Blue widget installation',
    'source'     => 'featured_post_context',
    'confidence' => 0.82,
]
```

### Review Workflow

- Review suggestions before applying them
- Apply individual suggestions
- Bulk-review multiple images
- Preserve empty alt text for intentionally decorative images
- Mark images as reviewed

### Future Ideas

- Optional AI-assisted suggestions
- AI image analysis through pluggable providers
- Accessibility guidance for decorative vs. meaningful images
- Bulk import/export
- WP-CLI support
- REST API endpoints
- Reporting and audit history
- Integration hooks for third-party plugins

## Installation

1. Download or clone this repository.
2. Copy the `alt-text-auditor` directory into:

   ```text
   /wp-content/plugins/
   ```

3. Activate **Alt Text Auditor** from the WordPress **Plugins** screen.
4. Open the Alt Text Auditor screen in the WordPress admin area.

## Project Structure

```text
alt-text-auditor/
├── alt-text-auditor.php
├── README.md
├── readme.txt
├── uninstall.php
├── src/
│   ├── Admin.php
│   ├── Auditor.php
│   └── SuggestionEngine.php
├── assets/
│   ├── css/
│   └── js/
└── .github/
    └── workflows/
```

The project intentionally uses a lightweight structure. It is designed to remain easy to understand while still separating auditing, suggestion generation, and admin UI responsibilities.

## Architecture

### `Auditor`

Responsible for locating image attachments that need review and collecting the metadata required by the admin interface.

Potential responsibilities include:

- Querying image attachments
- Reading `_wp_attachment_image_alt`
- Determining whether an image is a featured image
- Locating posts/pages that reference an image
- Returning normalized audit data

### `SuggestionEngine`

Responsible for generating candidate alt text from available WordPress data.

Example:

```php
$suggestion = $suggestion_engine->suggest( $attachment_id );
```

Possible return value:

```php
[
    'text'       => 'Blue widget installation',
    'source'     => 'filename',
    'confidence' => 0.65,
]
```

### `Admin`

Responsible for the WordPress admin experience, including:

- Audit tables
- Filters
- Review actions
- Suggestion approval
- Nonce and capability checks

## Accessibility Philosophy

Alt text should describe the purpose or meaning of an image in context, not simply repeat a filename or generate generic prose.

This plugin therefore treats suggestions as **recommendations**, not authoritative replacements.

Important principles include:

- Decorative images may correctly use an empty alt attribute.
- Context matters more than the image alone.
- Generated suggestions should always be reviewable.
- The plugin should not automatically overwrite meaningful existing alt text.
- Accessibility decisions should remain understandable to editors.

## Security

The plugin should follow standard WordPress security practices, including:

- Capability checks for administrative actions
- Nonce verification
- Input sanitization
- Output escaping
- Prepared database queries when direct queries are necessary
- No automatic external data transmission without explicit configuration

## Development Goals

This project is also intended to demonstrate practical WordPress engineering patterns, including:

- Object-oriented PHP
- WordPress hooks and filters
- Media Library and attachment metadata
- Admin UI development
- Accessibility-aware product design
- Secure data handling
- Unit and integration testing
- WordPress Coding Standards
- GitHub Actions / CI

## Development

Clone the repository:

```bash
git clone https://github.com/YOUR_GITHUB_USERNAME/alt-text-auditor.git
cd alt-text-auditor
```

If development dependencies are added later, installation instructions will be documented here.

## Roadmap

### 0.1.0

- Initial plugin bootstrap
- Missing-alt-text audit
- Admin list view
- Metadata-based suggestions
- Manual apply action

### 0.2.0

- Featured-image context
- Post/page usage detection
- Bulk review
- Suggestion confidence/source metadata

### 0.3.0

- Optional AI provider integration
- AI-assisted image/context analysis
- Decorative-image recommendations
- Audit history and reporting

## Contributing

Issues, suggestions, and pull requests are welcome.

If you are reporting a bug, please include:

- WordPress version
- PHP version
- Plugin version
- Steps to reproduce
- Expected behavior
- Actual behavior

## License

GPL-2.0-or-later

See the [GNU General Public License](https://www.gnu.org/licenses/gpl-2.0.html).

## Author

Marcello De Feo  
[marcellodefeo.com](https://marcellodefeo.com/]
