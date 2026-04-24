# LLM Wiki Template for Tech Sellers

A template for building a persistent, interlinked knowledge base to track client opportunities, contacts, contracts, and technical engagements using Bob (or any LLM) following the LLM Wiki pattern.

## What is LLM Wiki?

LLM Wiki is a pattern for maintaining a compounding knowledge base where:
- **Raw sources** (meeting notes, contracts, daily logs) remain immutable
- **Wiki pages** are LLM-generated, interlinked markdown documents
- **Every interaction** (ingest, query, lint) enriches the knowledge base
- **Cross-references** create a semantic graph of your client relationships and technical knowledge

## Quick Start

1. **Copy this template structure** to your project directory
2. **Copy `.bob/custom_modes.yaml`** from this template
3. **Customize domain context** in `.bob/custom_modes.yaml` (line 70) if needed
4. **Start adding sources** to `raw/` (meeting notes, daily logs)
5. **Tell Bob**: "Ingest raw/your-meeting-notes.md"

## Directory Structure

```
your-wiki/
├── .bob/
│   └── custom_modes.yaml          # Bob wiki mode configuration
├── raw/                            # Immutable source documents
│   ├── daily/                      # Daily activity logs
│   │   └── YYYY-MM-DD.md          # See SAMPLE-daily-log.md
│   └── [meeting-notes].md          # See SAMPLE-client-meeting.md
├── wiki/                           # LLM-generated knowledge pages
│   ├── [Client-Name].md            # See SAMPLE-Client-Name.md
│   └── [Technology-Name].md        # See SAMPLE-Technology-Name.md
├── index.md                        # Content catalog (see TEMPLATE-index.md)
└── log.md                          # Activity log (see TEMPLATE-log.md)
```

## Core Workflows

### 1. INGEST (Adding New Knowledge)
```
User: "Ingest raw/client-meeting-2024-03-15.md"

Bob will:
- Read the meeting notes
- Discuss key takeaways with you
- Create/update client pages, contact pages, technology pages
- Update index.md
- Add cross-references across 10-15 related pages
- Append entry to log.md
```

### 2. QUERY (Asking Questions)
```
User: "What's the status of our opportunity with Client XYZ?"
User: "Which clients are using Product A?"
User: "What are the key objections for Technology B?"

Bob will:
- Read index.md to find relevant pages
- Read identified wiki pages
- Synthesize answer with citations
```

### 3. LINT (Health Checks)
```
User: "Run a lint check"

Bob will:
- Check for contradictions, stale opportunity stages, missing cross-references
- Suggest follow-ups or information gaps
- Fix issues found
- Append summary to log.md
```

## What to Track

### Clients & Opportunities
- Client overview (industry, size, relationship)
- Current opportunities (stage, value, timeline)
- Technical environment and pain points
- Contract details and renewals
- Success criteria and risks

### Contacts
- Role and decision authority
- Priorities and concerns
- Relationship strength
- Recent interactions

### Products & Technologies
- Capabilities and use cases
- Technical details and integrations
- Positioning and competitive landscape
- Pricing and licensing
- Which clients use them

### Daily Activities
- Client meetings and calls
- Opportunities progressed
- Follow-ups completed
- Decisions and insights

## File Naming Conventions

### Raw Sources
- **Meeting notes**: `client-meeting-YYYY-MM-DD.md` or `ClientName-Topic-YYYY-MM-DD.md`
- **Daily logs**: `YYYY-MM-DD.md` in `raw/daily/`
- **Contracts**: `ClientName-Contract-YYYY-MM-DD.md`

### Wiki Pages
- **Clients**: `Client-Name.md` (Title-Case-With-Hyphens)
- **Contacts**: `Contact-Name.md`
- **Products**: `Product-Name.md`
- **Technologies**: `Technology-Name.md`

## Template Files Included

### Configuration
- `.bob/custom_modes.yaml` - Bob wiki mode configuration (copy to your `.bob/` directory)
- `.gitignore` - Protect sensitive client data from version control

### Templates
- `TEMPLATE-index.md` - Content catalog structure
- `TEMPLATE-log.md` - Activity log format with examples

### Sample Raw Sources
- `raw/SAMPLE-client-meeting.md` - Meeting notes template
- `raw/daily/SAMPLE-daily-log.md` - Daily log template

### Sample Wiki Pages
- `wiki/SAMPLE-Client-Name.md` - Client page format
- `wiki/SAMPLE-Contact-Name.md` - Contact page format
- `wiki/SAMPLE-Technology-Name.md` - Technology/product page format

## Setup Instructions

```bash
# 1. Create directory structure
mkdir -p raw/daily wiki .bob

# 2. Copy configuration
cp custom_modes.yaml .bob/custom_modes.yaml

# 3. Create initial files
cp TEMPLATE-index.md index.md
cp TEMPLATE-log.md log.md

# 4. Customize index.md with your categories (optional)

# 5. Add your first source
# Create raw/first-meeting-notes.md

# 6. Start Bob in Wiki mode and ingest
# "Ingest raw/first-meeting-notes.md"
```

## Best Practices

### Source Management
- Keep raw sources **immutable** - never edit after creation
- Use consistent date format: YYYY-MM-DD
- Capture meeting notes same day while fresh
- Daily logs help track activities and compound knowledge

### Wiki Maintenance
- Use relative links: `[Client Name](wiki/Client-Name.md)`
- Link liberally - connections are valuable
- Update opportunity stages regularly
- Keep contract renewal dates current
- Run lint every 10-20 ingests

### Cross-Referencing
- Every client page links to their contacts
- Every contact page links to their client
- Technology pages link to clients using them
- Meeting notes create/update multiple pages

## Example Session

```
User: "Ingest raw/acme-corp-meeting-2024-03-15.md"

Bob: [Reads meeting notes]

Key takeaways:
- Acme Corp evaluating Product X for data integration
- $500K opportunity, decision by April 30
- Technical POC needed with their Salesforce environment
- John Smith (CTO) is champion, Mary Johnson (VP Eng) has concerns about complexity

I'll create/update:
- wiki/Acme-Corp.md (new client page)
- wiki/John-Smith.md (new contact)
- wiki/Mary-Johnson.md (new contact)
- wiki/Product-X.md (update with new use case)
- wiki/Salesforce-Integration.md (update with requirements)
- index.md (add new pages)

Proceed?

User: "Yes"

Bob: [Creates 5 pages, updates index.md, appends to log.md]

Complete. 5 pages created, 12 cross-references added.
```

## Obsidian Integration (Optional)

1. Open this directory as an Obsidian vault
2. Enable graph view to visualize client/contact/technology relationships
3. Use Obsidian for browsing, Bob for maintenance
4. Your edits appear in real-time in both tools

## Security & Privacy

### Protecting Sensitive Data

This wiki may contain confidential client information. Follow these guidelines:

1. **Review `.gitignore`** - Customize to exclude sensitive files from version control
2. **Consider excluding `raw/`** - Uncomment in `.gitignore` if meeting notes contain confidential data
3. **Use generic names** - When sharing examples, anonymize client names
4. **Separate repositories** - Consider separate wikis for different security levels
5. **Access control** - Restrict repository access to authorized team members only

### Recommended Practices

- Don't commit API keys, passwords, or credentials
- Redact sensitive financial details before committing
- Use client codes instead of full names if required by policy
- Review diffs before committing to catch accidental sensitive data
- Consider encrypting the repository if it contains highly sensitive information

## Tips for Success

- **Start small**: Ingest 1-2 meeting notes to get comfortable
- **Daily logs compound**: Even brief daily notes add up over time
- **Query often**: Ask Bob questions to test your knowledge base
- **Lint regularly**: Keep the wiki healthy as it grows (every 10-20 ingests)
- **Cross-reference**: Connections are as valuable as content
- **Review security**: Regularly audit what's being committed to version control

Your wiki becomes more valuable with every client interaction you capture.