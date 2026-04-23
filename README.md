# 🤖 DIBOTAGENT - Discord AI Support Agent

> A powerful intelligent support bot for Discord built with .NET 8, powered by LLM models with RAG (Retrieval-Augmented Generation) capabilities.

DIBOTAGENT is a complete tool that allows you to create and manage intelligent Discord bots powered by AI. The bots use your own knowledge base (custom documents) through RAG to provide personalized support to your Discord community. It includes a web interface to manage projects, documents, bots, and configurations.

### 🔗 Official Repository

```
https://github.com/arkservertools/dibotagent
```

## 📑 Table of Contents

- [✨ Main Features](#-main-features)
- [⚙️ Requirements](#️-requirements)
- [🚀 Installation](#-installation)
- [📖 Quick Start Guide](#-quick-start-guide)
- [🎨 Web Interface](#-web-interface)
- [💡 Prompt Examples](#-prompt-examples)
- [🔧 Detailed Configuration](#-detailed-configuration)
- [📊 How DIBOTAGENT Works](#-how-dibotagent-works)
- [🎯 Best Practices](#-best-practices)
- [🆘 Troubleshooting](#-troubleshooting)
- [📚 Additional Resources](#-additional-resources)
- [📝 Changelog](#-changelog)

## ✨ Main Features

### 🎯 Project Management
- **Multiple knowledge bases**: Create different projects, each with its own configuration and knowledge base
- **Local storage**: All data is stored in your own local database (ChromaDB)
- **Customizable prompts**: Define the specific behavior of the AI for each project

### 📚 Document System (Knowledge Base)
- **Document upload**: Add text files to build the knowledge base for each project
- **Semantic search**: The AI searches for the most relevant information using embeddings
- **Optimized structure**: Supports titles, subtitles, lists and formatting for better understanding

### 🤖 Discord Bots (Multi-Bot)
- **Multiple bots**: Manage different bots across multiple Discord servers
- **Flexible behavior**:
  - **Monitored channels**: Bot responds only when specific roles/users are mentioned
  - **Open channels**: Bot responds to any message in the channel
  - **Private messages**: Configurable to respond or ignore DMs
- **Scheduled programming**: Define activity time slots for each bot
- **Monitored roles and users**: Control who can activate the bot

### 🔐 Access Management
- **User profiles**: Create users with different permission levels
- **Granular control**: Decide who can access which features
- **Secure authentication**: Web interface with customizable login

### 📊 History and Analytics
- **Complete logging**: All conversations are recorded
- **Historical queries**: Review previous conversations from the web interface
- **Interaction analysis**: Monitor how users interact with your bot

### 🧠 Supported AI Models
- **Ollama** (recommended for local): phi3.5, mistral, neural-chat, etc.
- **DeepSeek**: Cloud-based API (recommended for better performance)
- **Extensible**: Architecture prepared for future integrations (ChatGPT, Claude, etc.)
 
## ⚙️ Requirements

### Mandatory
- **Docker** (Linux, Docker Desktop for Windows & WSL)
- **ChromaDB** (vector database)
- **Ollama** (for embeddings and local LLM models) *OR* **DeepSeek API**

### Optional but Recommended
- **GPU**: For better performance with local AI models
- **DeepSeek Account**: Better performance and speed (very affordable)
- **Python** (only if you install Ollama locally without Docker)

### System Requirements
- **RAM**: Minimum 4GB (8GB recommended)
- **Storage**: Depends on the size of your knowledge base
- **Available port**: 8080/8081 for web interface

## 🚀 Installation

### Docker Compose (Recommended)

Docker Compose will automatically start DIBOTAGENT, ChromaDB, and Ollama in containers.

#### 1. Clone the repository

Clone the official DIBOTAGENT repository from GitHub:

```bash
git clone https://github.com/arkservertools/dibotagent.git
cd dibotagent
```

#### 2. Start the containers

```bash
docker compose up -d
```

This will start:
- **DIBOTAGENT** (web application)
- **ChromaDB** (vector database)
- **Ollama** (LLM server - optional if using DeepSeek)

#### 3. Install AI models

If using Ollama, install the recommended models:

```bash
# Install embeddings model (required for RAG)
docker exec -it ollama ollama pull nomic-embed-text

# Install LLM model (choose one)
docker exec -it ollama ollama pull phi3.5          # Recommended (4GB)
docker exec -it ollama ollama pull mistral         # More powerful (7GB)
docker exec -it ollama ollama pull neural-chat     # Lightweight (3GB)
docker exec -it ollama ollama pull gravestone      # Specialized
```

**⚠️ Important note**: If you change the embeddings model, you must create new projects and re-add the documents, as vectors are not compatible between models.

#### 4. Access the web interface

```
http://localhost:8080
```

Or with HTTPS:
```
https://localhost:8081
```

**Default credentials:**
- Username: `admin`
- Password: `admin123`

## 📖 Quick Start Guide

### 1. Create your first Project

1. Access the web interface (http://localhost:8080)
2. Go to **Projects** → **Create New**
3. Configure:
   - **Name**: E.g. "Technical Support"
   - **Description**: Define what type of questions it responds to
   - **Prompt**: Define the AI behavior (see examples below)
4. Save the project

### 2. Add Documents (Knowledge Base)

1. In the created project, go to **Documents** → **Upload New**
2. Add text files with your documentation:
   - FAQs (frequently asked questions)
   - Product/service guides
   - Policies and regulations
   - Tutorials
3. Structure documents with titles and subtitles for better search
4. Test queries in the **Test** tab to verify it finds relevant information

### 3. Create your First Discord Bot

1. Go to **Bots** → **Create New Bot**
2. Configure:
   - **Bot name**: Name visible in Discord
   - **Associated project**: The project created in step 1
   - **Bot token**: Your Discord bot token
3. Configure behavior:
   - **Monitored channels**: Which channels the bot operates in?
   - **Monitored roles**: Who can activate it?
   - **Schedule**: When is it active?
   - **Respond to DMs**: Does it respond to private messages?
4. Save and connect the bot to your Discord server

### 4. Test your Bot

1. Mention the bot in Discord in one of the configured channels
2. The bot will respond based on your knowledge base
3. Review conversations in **History** to monitor responses


## 🎨 Web Interface

The web interface provides a complete dashboard to manage all aspects of DIBOTAGENT.

### 📋 Projects

Projects are independent AI configurations, each with its own knowledge base.

**What is a Project:**
- Specific configuration of AI behavior (custom prompt)
- Unique knowledge base (collection of documents)
- Multiple bots can use the same project
- Allows different bots with different behaviors

**Use cases:**
- Technical support bot + Customer service bot (2 projects)
- Multi-language bot (1 project per language)
- General bot vs Specialized bot (2 different projects)

**Project Configuration:**

| Option | Description |
|--------|-------------|
| Name | Unique project identifier |
| Description | What type of support it provides |
| Prompt | Instructions for AI behavior |
| LLM Model | AI model to use (phi3.5, mistral, etc.) |
| Temperature | Creativity control (0-1) |

### 📄 Documents

Documents form the knowledge base that the AI consults to answer questions.

**Recommended document types:**
- 📖 **Documentation**: Usage guides, tutorials
- ❓ **FAQs**: Frequently asked questions and answers
- 📋 **Policies**: Terms, rules, regulations
- 🔧 **Technical specifications**: Features, limitations
- 📞 **Contact information**: Departments, hours, links

**Best practices:**

✅ **Well structured:**
```
# Main Title (H1)
## Subtitle (H2)
### Subsection (H3)

- Point 1
- Point 2
- Point 3

**Important information**: highlight in bold
```

✅ **Relevant description**: Each document should have a clear description of its content

✅ **Updates**: Keep documents updated for accurate responses

❌ **Avoid**: Very long documents without structure, duplicate information, disorganized content

### 👥 Profiles and Users

Manage who can access the web interface and what they can do.

**Profile Types:**
- **Admin**: Full access to all features
- **Editor**: Can create/edit projects and documents
- **Viewer**: Read-only access to history
- **Custom**: Define your own permissions

**Security Considerations:**
- Change default password immediately
- Use strong passwords (minimum 12 characters)
- Limit number of admins
- Review access regularly

### 🤖 Discord Bots

Manage multiple bots across different Discord servers.

**Essential Configuration:**

| Parameter | Description | Example |
|-----------|-------------|---------|
| **Bot name** | Visible in Discord | `SupportBot` |
| **Project** | Knowledge base to use | `Technical Support` |
| **Token** | Discord bot token | From Developer Portal |

**Bot Behavior:**

- **Monitored channels**: Channels where bot is active
- **Monitored mode**: Bot responds only when mentioned (efficient)
- **Open mode**: Bot responds to everyone (more interactive)
- **Monitored roles**: Only responds when certain roles are mentioned
- **Monitored users**: Only responds when specific users are mentioned

**Advanced Configuration:**

```yaml
Schedule:
  - Monday to Friday: 09:00 - 18:00
  - Saturday: 10:00 - 14:00
  - Sunday: Disabled

Private Messages:
  - Respond to DMs: Yes/No
  - Project for DMs: (can be different)
  - Messages per hour: Rate limiting

Behavior:
  - Keep history: Last N messages
  - Mention users: Automatic with @user
  - Write indicators: Show typing indicator
```

### ⚙️ General Configuration

**Ollama:**
- API URL
- LLM and embeddings models
- Token limit
- Connection timeout

**ChromaDB:**
- Host and port
- API Key (if applicable)
- Number of fragments to retrieve (Top K)
- Maximum similarity distance (0-1)

**DeepSeek:**
- API Key
- Selected model
- Temperature and max tokens
- Timeout

### 📊 History

View all conversations between users and bots.

**Features:**
- 🔍 Filter by bot, user, date
- 📅 Custom date range
- 💬 View complete conversation with context
- ⭐ Mark important conversations
- 📥 Export conversations

**Use cases:**
- Monitor response quality
- Identify frequent topics
- Improve documentation based on questions
- Satisfaction analysis

## 💡 Prompt Examples

Prompts define how the AI behaves. Here are examples for different cases:

### 📝 Simple Prompt

Perfect for getting started, flexible and simple:

```
DESCRIPTION:
Your function is to provide help and support to users of [YOUR SERVER].
You are a friendly and professional Discord administrator.

CRITICAL INSTRUCTIONS:
1. ONLY use information from 'AVAILABLE INFORMATION'
2. If no information: "I don't have information about this"
3. Don't invent or make assumptions
4. Be precise and cite the source of information
5. Use the HISTORY to understand context
6. Today is {datetime} UTC, keep that in mind for dates

CONVERSATION HISTORY:
{discord_conversation_content}

AVAILABLE INFORMATION:
{documents_content}

QUESTION:
{user_question}

ANSWER:
```

### 🎯 Advanced Prompt

More control over behavior and mentions:

```
DESCRIPTION AND FUNCTION:
Your function is to provide help and support to the community of [MY SERVER].
You are a professional and efficient Discord administrator.

CRITICAL RULES:
1. If the question is NOT related to [Your server name] or doesn't appear in 'AVAILABLE INFORMATION', or you have no answer in the CONVERSATION HISTORY, respond politely that you have no information about it.
2. If NO information: 'I don't have information about this in the documents'
3. Be precise and cite information from documents
4. Use CONVERSATION HISTORY to understand context
5. Today is {datetime} UTC in your timezone, keep that in mind for date-related questions
6. Your bot ID is {botid}
7. Respond to users based on CONVERSATION HISTORY and AVAILABLE INFORMATION provided
8. If you address someone from history or who asked you, ALWAYS use their Discord mention ID: <@ID>
9. The ID of the user asking you is {discordid}
10. If you want to mention this user, write exactly: <@{discordid}>
11. If you see other IDs in history like [ID: 12345] and want to refer to them, write: <@12345>
12. NEVER write just the name, always use <@ID> format so Discord mentions the users correctly
13. In history you'll see your own responses marked as 'IABOT' with ID {botid}, analyze what others said and what YOU responded before to not be redundant
14. When someone talks to you, you'll see the tag IABOT<@{botid}>. That means they're talking directly to you
15. If a user asks you something you already answered, you can reference your previous message or simply answer again with more detail

TOPIC FILTER:
Don't invent or make assumptions.
If a user asks an administrator for help and the answer doesn't appear in available information, tell them to open a support ticket with all necessary information
HUMAN TONE:
Write naturally, like in a chat. Use short sentences, avoid perfect numbered lists and don't use 'AI Assistant' language. You can use occasional emoji.
Don't write giant paragraphs. On Discord people read quickly.
If the answer is technical, simplify it. If it's an instruction, be direct.

RESTRICTIONS:
- NEVER write just the name, always use <@ID>
- Don't mention you're an AI
- Be natural, like chatting on Discord
- Don't use giant paragraphs, short sentences
- Don't repeat the same phrase always

IF YOU HAVE DOUBTS:
"I don't have information about this in the documents"

CONVERSATION HISTORY:
{discord_conversation_content}

AVAILABLE INFORMATION:
{documents_content}

CURRENT QUESTION:
User:  {discordname}<@{discordid}>
Message: {user_question}

ANSWER:
```

### 🎓 Technical Support Prompt

Specialized for technical problems:

```
ROLE:
You are a support technician specialized in [PRODUCT/SERVICE].
Your goal is to help users solve technical problems.

INSTRUCTIONS:
1. Diagnose the problem by asking if necessary
2. Provide step-by-step solutions
3. If too complex, direct to support ticket
4. Verify that the solution worked
5. Don't assume user configurations
6. Suggest best practices when relevant

AVAILABLE INFORMATION:
{documents_content}

PREVIOUS CONVERSATION:
{discord_conversation_content}

QUESTION:
{user_question}

ANSWER:
```

### 🌍 Multi-language Prompt

For bots in multi-language servers:

```
LANGUAGE:
Always respond in the language of the question.
If in Spanish, respond in Spanish.
If in English, respond in English.

FUNCTION:
You are an international support assistant.
Your goal is to help users from different countries.

INSTRUCTIONS:
1. Detect the language of the question
2. Respond in that language
3. Be formal but friendly
4. Adapt hours and references to local contexts
5. Only use documented information

AVAILABLE INFORMATION:
{documents_content}

QUESTION:
{user_question}

ANSWER:
```



## 🔧 Detailed Configuration

### Ollama Configuration

**Important Parameters:**

| Parameter | Range | Description |
|-----------|-------|-------------|
| **Ollama URL** | URL | Ollama API endpoint (e.g: http://localhost:11434) |
| **Model** | string | LLM model to use (must be installed) |
| **Embedding URL** | URL | Embeddings endpoint (usually same as Ollama URL) |
| **Embedding Model** | string | Model for vectorizing documents (e.g: nomic-embed-text) |
| **Embedding Word Max Size** | numbers | Maximum words per embedding (approx. 250 if token limit is 512) |
| **Num Predict** | 128-4096 | Maximum tokens in response (higher = longer responses) |
| **Http Timeout** | seconds | Wait timeout for Ollama responses |

**Recommended Models:**

```yaml
Embeddings:
  - nomic-embed-text: Fast, 768 dimensions, recommended
  - all-minilm: Lightweight, good precision
  - mxbai-embed-large: More powerful, slower

LLM:
  - phi3.5: 4GB RAM, very efficient
  - mistral: 7GB RAM, better quality
  - neural-chat: 5GB RAM, chat-specific
  - gravestone: Game-specialized
```

### ChromaDB Configuration

| Parameter | Range | Description |
|-----------|-------|-------------|
| **ChromaDB Host** | host:port | Server address (e.g: localhost:8000) |
| **ChromaDB Api Key** | string | API key (optional, only if secured) |
| **Top K Fragments** | 1-20 | Document fragments to retrieve (5-10 recommended) |
| **Max Fragments Distance** | 0.0-1.0 | Minimum similarity (0=identical, 1=different. Use 0.3-0.7) |
| **Http Timeout** | seconds | Timeout for ChromaDB queries |

**Distance Guide:**
- `0.2` - Very restrictive, only exact matches
- `0.4` - Recommended, good precision
- `0.6` - More permissive, more results
- `0.8` - Very permissive, may bring irrelevant ones

### DeepSeek Configuration

**⭐ RECOMMENDED**: DeepSeek API offers better performance and is very affordable.

| Parameter | Range | Description |
|-----------|-------|-------------|
| **API Key** | string | Your DeepSeek API key |
| **Model** | string | Model (deepseek-chat or deepseek-coder) |
| **Temperature** | 0.0-2.0 | Creativity control (0=deterministic, 1=normal, >1=creative) |
| **Max Tokens** | 100-4000 | Maximum response length |
| **Http Timeout** | seconds | Timeout for responses |

**Recommended temperature by case:**
- `0.3` - Technical support, precise answers
- `0.7` - General support, balanced
- `1.0` - Conversational, creative

## 📊 How DIBOTAGENT Works

### Operation Flow

```
User asks in Discord
        ↓
Bot receives message
        ↓
Is it in monitored channel?        Is response allowed?
        ↓                                   ↓
Searches similar embeddings in ChromaDB
        ↓
Gets relevant document fragments
        ↓
Builds prompt with:
  - Project instructions
  - Relevant fragments
  - Conversation history
  - User question
        ↓
Sends to LLM model (Ollama or DeepSeek)
        ↓
Receives generated response
        ↓
Saves to history
        ↓
Sends response to Discord
```

### Two Operation Modes

**1️⃣ MONITORED MODE (Recommended for support)**

```
Bot responds only when:
✓ Specific roles/users are mentioned
✓ Bot is directly cited
✓ Mentioned in specific channels

Advantages:
- More control
- Less spam
- Better for dedicated support
- Lower resource consumption
```

**2️⃣ OPEN MODE**

```
Bot responds to:
✓ All messages in the channel
✓ Without need for mention
✓ Remembering conversation with each user

Advantages:
- More interactive
- Better UX for casual users
- More natural conversations
- Requires better document configuration
```

### Conversation Persistence

The bot maintains context at two levels:

**At channel level**: Remembers last N messages for context
**At user level**: Maintains conversation with specific user while active

If user leaves, context is lost after X configured time.

## 🎯 Best Practices

### ✅ For Documents

1. **Clear structure**
   - Use hierarchical headings (H1, H2, H3)
   - Group related information
   - Use lists for multiple items

2. **Relevant content**
   - Write as if for search (keywords)
   - Avoid duplicate information
   - Keep updated

3. **Descriptions**
   - Describe what each document contains
   - Use words users would search for
   - Be specific (not: "document", yes: "FAQ connection issues")

### ✅ For Prompts

1. **Be explicit**
   - Define AI role clearly
   - Indicate what it MUST and MUST NOT do
   - Be specific with instructions

2. **Important context**
   - Always include {documents_content}
   - Always include {discord_conversation_content}
   - Use system variables ({datetime}, {botid}, etc.)

3. **User mentions**
   - Teach bot `<@ID>` format
   - Be explicit about when to mention
   - Provide examples

### ✅ For Discord Bots

1. **Sensible configuration**
   - Channels: Only where support is needed
   - Roles: Users who can activate it
   - Schedule: When staff is available

2. **Rate limiting**
   - Set message limit per hour
   - Avoid response spam
   - Protect resources

3. **Monitoring**
   - Review history regularly
   - Improve prompts based on responses
   - Update documents based on frequent questions

## 🆘 Troubleshooting

### Bot doesn't respond

**Check:**
- ✓ Bot is connected to Discord (valid token)
- ✓ Bot has read/write permissions in channel
- ✓ Within configured schedule
- ✓ In monitored channel or configured as open
- ✓ AI model is running (Ollama or DeepSeek)

**Check logs:**
```bash
docker logs dibotagent
docker logs ollama  # if using Ollama
```

### Slow responses

**Common causes:**
- AI model too heavy (switch to lighter one)
- Slow network (optimize Ollama or use DeepSeek API)
- ChromaDB slow (reduce Top K Fragments)
- GPU not available (configure Ollama with GPU)

**Solutions:**
```bash
# Switch to lighter model
docker exec -it ollama ollama pull phi3
docker exec -it ollama ollama rm phi3.5

# If using GPU, check availability
docker exec -it ollama nvidia-smi  # For NVIDIA
```

### Incompatible vectors

**Problem**: Changed embeddings model but still using old vectors

**Solution**: 
- Create new project
- Re-add documents
- New vectors will be created with new model

### Documents not found

**Check:**
- ✓ Document description is clear
- ✓ Content contains words user searches for
- ✓ Structure is correct (with titles)
- ✓ Top K Fragments is sufficient (>= 5)
- ✓ Max Distance is not too restrictive (0.3-0.5)

**Debug:**
- Test queries in "Test" section of web
- Check what fragments are returned
- Adjust Max Distance if needed

## 📚 Additional Resources

- [Discord Developer Portal](https://discord.com/developers/applications)
- [Ollama Models](https://ollama.ai/library)
- [DeepSeek Docs](https://platform.deepseek.com/api-docs)
- [ChromaDB Documentation](https://docs.trychroma.com)
- [RAG Concepts](https://en.wikipedia.org/wiki/Retrieval-augmented_generation)

## 📝 Changelog

| Version | Changes |
|---------|---------|
| **1.0.1** | Removed API controllers |
| **1.0.0** | Initial release |

## 📄 License

DIBOTAGENT is licensed under **AGPL-3.0 (GNU Affero General Public License v3.0)**

This means:

- ✅ **Allowed**: Personal and private use
- ✅ **Allowed**: Modification and distribution
- ✅ **Allowed**: Use on private servers
- ✅ **Allowed**: Community contributions and improvements
- ❌ **NOT Allowed**: Commercial sale of software
- ❌ **NOT Allowed**: Commercial use without explicit author authorization
- ❌ **NOT Allowed**: Privatizing modifications without sharing source code
- ⚠️ **Required**: If you offer DIBOTAGENT as a network service, you must provide access to source code

For more information about AGPL-3.0 license, visit: https://www.gnu.org/licenses/agpl-3.0.html

For inquiries about commercial licenses, contact the project owners in the official repository.

## 🤝 Contributions

Contributions are welcome. Please open an issue or pull request.

## 💬 Support

For help:
1. Review the [Troubleshooting](#-troubleshooting)
2. Check the [History](#-history) of conversations
3. Open an issue in the repository

---

**Made with ❤️ for the Discord community**

