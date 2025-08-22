# Documentation Guide for Rush2.ai

## 📚 Documentation Stack

### 1. Mintlify (Primary Documentation)
- **Purpose**: User-facing documentation, API reference, guides
- **Location**: `/docs` directory
- **Format**: MDX (Markdown with JSX)
- **Live Preview**: `npm run docs:dev` (http://localhost:3333)
- **Deployment**: Auto-deploys to docs.rush2.ai on push to main

### 2. Swimm (Code Documentation)
- **Purpose**: Team-internal code documentation, onboarding
- **Location**: `.swm` directory
- **Features**: 
  - Code coupling documentation
  - Live code snippets
  - Automatic sync with code changes
  - PR documentation requirements

### 3. JSDoc (Inline Documentation)
- **Purpose**: Function and API documentation
- **Location**: Inline with code
- **Auto-generation**: `npm run docs:generate`

## 📝 Documentation Standards

### File Naming
- User guides: `kebab-case.mdx`
- API endpoints: `endpoint-name.mdx`
- Code docs: `PascalCase.md` for components

### MDX Front Matter
```yaml
---
title: 'Page Title'
description: 'Brief description for SEO'
sidebarTitle: 'Shorter title' # Optional
'og:image': '/images/og-image.png' # Optional
---
```

### Component Documentation Template
```typescript
/**
 * Component description
 * 
 * @component
 * @example
 * ```tsx
 * <ComponentName prop="value" />
 * ```
 * 
 * @param {Object} props - Component props
 * @param {string} props.prop1 - Description of prop1
 * @param {number} [props.prop2=defaultValue] - Optional prop2
 * @returns {JSX.Element} Rendered component
 * 
 * @see {@link https://docs.rush2.ai/components/component-name}
 * @since 1.0.0
 */
```

### API Endpoint Documentation Template
```typescript
/**
 * @api {post} /api/endpoint Endpoint Title
 * @apiName EndpointName
 * @apiGroup GroupName
 * @apiVersion 1.0.0
 * 
 * @apiDescription
 * Detailed description of what this endpoint does
 * 
 * @apiParam {String} param1 Description of param1
 * @apiParam {Number} [param2] Optional param2
 * 
 * @apiSuccess {Boolean} success Success status
 * @apiSuccess {Object} data Response data
 * 
 * @apiError {String} error Error message
 * @apiError {Number} code Error code
 * 
 * @apiExample {curl} Example usage:
 * curl -X POST https://api.rush2.ai/v1/endpoint \
 *   -H "Authorization: Bearer TOKEN" \
 *   -d '{"param1": "value"}'
 */
```

## 🔄 Documentation Workflow

### 1. When Adding New Features
1. Update relevant `.mdx` files in `/docs`
2. Add JSDoc comments to new functions/components
3. Create Swimm doc if it's a complex feature
4. Run `npm run docs:check` to verify links

### 2. When Modifying APIs
1. Update endpoint documentation
2. Run `npm run docs:generate` to regenerate
3. Update examples if needed
4. Check OpenAPI spec if applicable

### 3. Before Committing
```bash
# Check documentation
npm run docs:check

# Generate API docs
npm run docs:generate

# Preview changes
npm run docs:dev
```

### 4. PR Documentation Checklist
- [ ] Updated relevant documentation
- [ ] Added JSDoc for new functions
- [ ] Updated API documentation if needed
- [ ] Checked for broken links
- [ ] Added examples for new features

## 🚀 Quick Commands

```bash
# Start documentation server
npm run docs:dev

# Build documentation
npm run docs:build

# Check for broken links
npm run docs:check

# Generate API documentation
npm run docs:generate

# Update all documentation
npm run docs:update
```

## 📦 Documentation Structure

```
docs/
├── introduction.mdx          # Landing page
├── quickstart.mdx            # Getting started
├── development.mdx           # Development guide
├── api-reference/
│   ├── introduction.mdx      # API overview
│   ├── authentication.mdx    # Auth guide
│   └── endpoint/             # Endpoint docs
│       ├── auth.mdx
│       ├── brands.mdx
│       ├── content.mdx
│       ├── images.mdx
│       └── videos.mdx
├── core/                     # Core concepts
│   ├── multi-tenancy.mdx
│   ├── brand-management.mdx
│   ├── content-generation.mdx
│   └── security.mdx
├── developer/                # Developer guides
│   ├── setup.mdx
│   ├── environment.mdx
│   ├── database.mdx
│   ├── testing.mdx
│   └── deployment.mdx
└── architecture/             # Architecture docs
    ├── overview.mdx
    ├── tech-stack.mdx
    ├── data-model.mdx
    ├── api-design.mdx
    └── security-model.mdx
```

## 🎨 Mintlify Components

### Cards
```mdx
<Card title="Title" icon="icon-name" href="/link">
  Description text
</Card>
```

### Card Groups
```mdx
<CardGroup cols={2}>
  <Card>...</Card>
  <Card>...</Card>
</CardGroup>
```

### Steps
```mdx
<Steps>
  <Step title="First Step">
    Content for first step
  </Step>
  <Step title="Second Step">
    Content for second step
  </Step>
</Steps>
```

### Code Blocks
```mdx
```typescript
// TypeScript code
```

```bash
# Bash commands
```
```

### Tabs
```mdx
<Tabs>
  <Tab title="Tab 1">
    Content 1
  </Tab>
  <Tab title="Tab 2">
    Content 2
  </Tab>
</Tabs>
```

### Callouts
```mdx
<Note>
  Important information
</Note>

<Warning>
  Warning message
</Warning>

<Info>
  Informational content
</Info>
```

## 🔗 External Resources

- [Mintlify Documentation](https://mintlify.com/docs)
- [Swimm Documentation](https://docs.swimm.io)
- [JSDoc Reference](https://jsdoc.app)
- [MDX Documentation](https://mdxjs.com)

## 📊 Documentation Metrics

Track documentation health:
- Coverage: Aim for 100% of public APIs documented
- Freshness: Update within 24h of code changes
- Accessibility: Check readability scores
- Completeness: Include examples for all features

## 🤝 Contributing to Documentation

1. Follow the templates above
2. Use clear, concise language
3. Include practical examples
4. Test all code snippets
5. Request review from team lead

---

*Remember: Good documentation is as important as good code!*