# LLM Wiki Template for Tech Sellers

A template for building a persistent, interlinked knowledge base to track client opportunities, contacts, contracts, and technical engagements using Bob (or any LLM) following the LLM Wiki pattern.

## Prerequisites

Before getting started, you'll need:

- **Bob AI Assistant** - Installed in VS Code ([Get Bob](https://bob.ibm.com/))

Optional but recommended:
- **Obsidian** - For visualizing your knowledge graph ([Download Obsidian](https://obsidian.md/))

## What is LLM Wiki?

LLM Wiki is a pattern for maintaining a compounding knowledge base where:
- **Raw sources** (meeting notes, contracts, daily logs) remain immutable
- **Wiki pages** are LLM-generated, interlinked markdown documents
- **Every interaction** (ingest, query, lint) enriches the knowledge base
- **Cross-references** create a semantic graph of your client relationships and technical knowledge

## Quick Start

1. Clone or copy this template to your project directory
2. Verify `.bob/custom_modes.yaml` is present (already included in template)
3. Switch Bob to CSE-LLM-WIKI mode:
   - Open Bob
   - Select "📚 CSE-LLM-WIKI" from the list of modes
4. Customize domain context (optional): Edit `.bob/custom_modes.yaml` line 70 if needed
5. Create your first source document in `raw/` (see `raw/SAMPLE-client-meeting.md` for inspiration)
6. Tell Bob: "Ingest raw/your-meeting-notes.md"
7. Bob will discuss key takeaways and ask for confirmation before creating wiki pages

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


**Note:** Don't create wiki files yourself. Bob will create actual wiki pages when you ingest your first source document.

## Setup Instructions

```bash
# 1. Clone or copy this template to your project directory
# The directory structure is already set up for you

# 2. Verify the structure exists
ls -la  # Should see: .bob/, raw/, wiki/, TEMPLATE-*.md files

# 3. Create initial files from templates
cp TEMPLATE-index.md index.md
cp TEMPLATE-log.md log.md

# 4. (Optional) Customize domain context in .bob/custom_modes.yaml
# Edit line 70 if you want to change from CSE/tech sales focus

# 5. Create your first source document
# Use raw/SAMPLE-client-meeting.md as inspiration
# Example: raw/my-first-meeting-2024-03-15.md

# 6. Open Bob and switch to CSE-LLM-WIKI mode
# In Bob, select "📚 CSE-LLM-WIKI" from modes list

# 7. Start your first ingest
# Tell Bob: "Ingest raw/my-first-meeting-2024-03-15.md"
# Bob will read it, discuss findings, and create wiki pages
```

## Best Practices

### Source Management
- Keep raw sources **immutable** 
- Use consistent date format: YYYY-MM-DD
- Capture meeting notes same day while fresh
- Daily logs help track activities and compound knowledge

### Wiki Maintenance
- Use relative links: `[Client Name](wiki/Client-Name.md)`
- Link liberally - connections are valuable
- Update opportunity stages regularly
- Run lint every 10-20 ingests

### Cross-Referencing
- Every client page links to their contacts
- Every contact page links to their client
- Technology pages link to clients using them
- Meeting notes create/update multiple pages

## First Ingest Walkthrough

Here's what happens when you ingest your first document:

```
User: "Ingest raw/acme-corp-meeting-2024-03-15.md"

Bob: [Reads the meeting notes]

Key takeaways from the meeting:
- Acme Corp is evaluating Product X for data integration
- $500K opportunity, decision timeline: April 30
- Technical POC needed with their Salesforce environment
- John Smith (CTO) is the champion
- Mary Johnson (VP Eng) has concerns about complexity

I'll create/update these wiki pages:
- wiki/Acme-Corp.md (new client page)
- wiki/John-Smith.md (new contact)
- wiki/Mary-Johnson.md (new contact)
- wiki/Product-X.md (update with new use case)
- wiki/Salesforce-Integration.md (update with requirements)
- index.md (add new pages to catalog)
- log.md (record this ingest)

Proceed with creating these pages?

User: "Yes"

Bob: [Creates/updates pages with cross-references]

✓ Created 3 new pages, updated 2 existing pages
✓ Added 12 cross-references between related pages
✓ Updated index.md with new entries
✓ Logged activity to log.md

Your wiki now has 5 pages with interconnected knowledge about Acme Corp.
```


## Obsidian Integration (Optional)

1. Open this directory as an Obsidian vault
2. Enable graph view to visualize client/contact/technology relationships
3. Use Obsidian for browsing, Bob for maintenance
4. Your edits appear in real-time in both tools

## Security & Privacy

### Protecting Sensitive Data

This wiki may contain confidential client information. Follow these guidelines:

1. Review `.gitignore` - Customize to exclude sensitive files from version control (Don't commit API keys, passwords, or credentials)
2. Access control - Restrict repository access to authorized team members only. Consider encrypting the repository if it contains highly sensitive information
3. Review diffs before committing to catch accidental sensitive data

## Tips for Success

- Start small: Ingest 1-2 meeting notes to get comfortable
- Daily logs compound: Even brief daily notes add up over time
- Query often: Ask Bob questions to test your knowledge base
- Lint regularly: Keep the wiki healthy as it grows (every 10-20 ingests)
- Cross-reference: Connections are as valuable as content
- Review security: Regularly audit what's being committed to version control

Your wiki becomes more valuable with every client interaction you capture.