# Company Website — Strapi CMS

Strapi-based headless CMS for the Company Website project.

The CMS manages editable website content and exposes it through Strapi's REST API to the Next.js frontend.

## Documentation

The broader application documentation is maintained in the Next.js frontend project.

- Architecture — application architecture and design decisions
- CMS Guide — CMS models, content management, and integration
- Development Guide — local setup, development workflow, and Git conventions

## Tech Stack

- Strapi 5
- Node.js
- TypeScript
- SQLite for local development
- REST API
- Strapi Media Library

## CMS Responsibilities

The Strapi application is responsible for:

- Managing editable website content
- Providing REST APIs
- Managing media assets
- Providing the Strapi administration panel
- Persisting CMS content
- Managing published content

The Next.js application is responsible for presentation, rendering, routing, and frontend behavior.

## Content Types

### Site Settings

A Single Type used for global website information.

Current fields:

- `companyName`
- `logo`
- `footerText`
- `mission`
- `vision`

API:

```text
GET /api/site-setting
```

### Services

A Collection Type used to manage company services.

Current fields:

- `title`
- `description`
- `price`
- `image`

API:

```text
GET /api/services
```

For service images:

```text
GET /api/services?populate=image
```

### Team Members

A Collection Type used to manage team members.

Current fields:

- `name`
- `role`
- `bio`
- `photo`

### Blog Posts

A Collection Type used for blog content.

Current fields:

- `title`
- `slug`
- `excerpt`
- `coverImage`
- `publishedDate`
- `content`

Blog posts are accessed using their slug from the Next.js frontend.

### Homepage

The CMS contains a homepage content model used to manage homepage-specific content.

## Media

Strapi's Media Library manages uploaded media used by content types such as:

- Service images
- Team member photos
- Blog cover images
- Site logo
- Homepage media

The Next.js frontend consumes the media URLs returned by the Strapi API.

## Local Development

Install dependencies:

```bash
npm install
```

Start Strapi in development mode:

```bash
npm run develop
```

The Strapi administration panel is available at:

```text
http://localhost:1337/admin
```

The REST API is available at:

```text
http://localhost:1337/api
```

## Environment Variables

Create a local environment file:

```text
.env
```

Never commit real secrets.

Use `.env.example` to document the required environment variables.

Typical Strapi environment variables include:

```env
HOST=0.0.0.0
PORT=1337

APP_KEYS=
API_TOKEN_SALT=
ADMIN_JWT_SECRET=
TRANSFER_TOKEN_SALT=
JWT_SECRET=
```

Values above are examples only. Use the environment variables generated/configured for the project.

## Content Workflow

When adding or changing content:

1. Start the Strapi application.
2. Open the Strapi administration panel.
3. Create or update the content.
4. Publish the content when appropriate.
5. Verify the REST API response.
6. Verify the content in the Next.js frontend.

## API Integration

The Next.js application follows this integration flow:

```text
Next.js Page
     ↓
Resource Service
     ↓
cmsFetch()
     ↓
Strapi REST API
```

Examples of resource services in the frontend include:

```text
lib/cms/site.ts
lib/cms/services.ts
lib/cms/team.ts
lib/cms/blog.ts
```

The CMS owns content and data.

The Next.js application owns presentation and rendering.

## Content vs Presentation

Content that should be editable by content administrators belongs in Strapi.

Examples:

- Company name
- Mission
- Vision
- Services
- Team members
- Blog posts
- Images
- Homepage content

Presentation concerns remain in Next.js.

Examples:

- Layout
- Responsive behavior
- Tailwind CSS classes
- Component structure
- Animations
- Rendering strategy

## API Verification

When adding a new content type:

1. Create the content type in Strapi.
2. Create sample content.
3. Publish the content.
4. Verify the REST API response.
5. Determine the actual response shape.
6. Create the corresponding TypeScript contract in Next.js.
7. Implement the resource service.
8. Integrate it into the required page or component.

Do not assume the API response shape without verifying it.

## Production Considerations

The current CMS is primarily configured for local development and training.

Before production deployment, review:

- Production database configuration
- Secrets management
- CORS
- API permissions
- Admin security
- Authentication
- Media storage
- Database backups
- Logging
- Monitoring
- Deployment configuration
- Production environment variables

## Project Relationship

The CMS is consumed by the Next.js company website.

```text
Browser
   ↓
Next.js
   ↓
CMS Service Layer
   ↓
Strapi REST API
   ↓
Database
```

Strapi provides the content.

Next.js provides the website experience.

## Repository Structure

The main Strapi project structure is:

```text
company-cms/
├── config/
├── database/
├── public/
├── src/
│   ├── admin/
│   ├── api/
│   │   ├── blog/
│   │   ├── homepage/
│   │   ├── service/
│   │   ├── site-setting/
│   │   └── team/
│   └── ...
├── types/
├── .env.example
├── .gitignore
├── package.json
├── package-lock.json
├── README.md
└── tsconfig.json
```

Generated/runtime directories such as `node_modules`, `.tmp`, `.cache`, and build output should not be committed.

## Git Workflow

The repository uses the following workflow:

```text
develop
   ↓
feature branch
   ↓
implementation
   ↓
verification
   ↓
commit
   ↓
push
   ↓
Pull Request → develop
   ↓
review
   ↓
merge
   ↓
update develop
```

Keep commits focused and use descriptive commit messages.

## License

This project is for learning and development purposes.
