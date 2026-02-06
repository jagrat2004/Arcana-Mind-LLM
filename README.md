# 🔮 Magician-Arcana-LLM Application

A modern, AI-powered tarot reading application that combines the ancient wisdom of tarot with cutting-edge language models. This interactive tool generates personalized tarot readings with detailed interpretations, symbolism analysis, and psychological insights.

## ✨ Features

- **Interactive Web Interface**: Built with Streamlit for a user-friendly, responsive experience
- **Customizable Card Spreads**: Choose between 3, 5, or 7-card spreads for different depths of insight
- **AI-Powered Interpretations**: Uses local LLM (Ollama with phi3:mini) to generate contextual tarot readings
- **Card Reversal System**: Randomly reverses cards for nuanced interpretations (reversed cards appear upside down)
- **Visual Card Display**: Beautiful card images displayed dynamically with orientation
- **Comprehensive Card Database**: 78 traditional tarot cards with detailed meanings, reversals, and symbolism
- **Context-Aware Readings**: Personalizes interpretations based on user's specific question or life situation
- **Psychological Integration**: Combines tarot symbolism with psychological advice

## 🔧 Architecture & How It Works

### System Architecture Diagram

![System Architecture](data/readme/system_architecture.png)


## 📋 Prerequisites

Before you begin, ensure you have the following installed:

- **Python 3.8+**: [Download Python](https://www.python.org/downloads/)
- **Ollama**: [Download Ollama](https://ollama.ai/) - Local LLM runtime
- **phi3:mini Model**: Download via Ollama (`ollama pull phi3:mini`)

### System Requirements

- **RAM**: Minimum 4GB (8GB+ recommended for smooth LLM performance)
- **Disk Space**: ~3GB for Ollama models
- **Internet Connection**: Required for initial setup (can run offline after setup)

## 🚀 Quick Start

### Step 1: Clone/Setup the Project

```bash
# Navigate to your project directory
cd chat-with-tarots
```

### Step 2: Create a Virtual Environment (Recommended)

```bash
# Windows
python -m venv venv
venv\Scripts\activate

# macOS/Linux
python -m venv venv
source venv/bin/activate
```

### Step 3: Install Dependencies

```bash
pip install -r requirements.txt
```

**Required Packages:**
- `streamlit` - Modern web framework for data apps
- `pandas` - Data manipulation and CSV processing
- `langchain` - LLM orchestration framework
- `langchain-core` - Core LangChain utilities
- `langchain-ollama` - Ollama integration for LangChain
- `ollama` - Python client for Ollama
- `pillow` - Image processing (PIL)

### Step 4: Start Ollama Service

```bash
# Open a separate terminal and start Ollama
ollama serve

# In another terminal, pull the phi3:mini model (one-time)
ollama pull phi3:mini
```

### Step 5: Run the Application

```bash
streamlit run app.py
```

The application will open in your default browser at `http://localhost:8501`

## 📖 How to Use

### Basic Usage

1. **Select Card Spread**: Choose between 3, 5, or 7 cards
   - **3 cards**: Focused reading for specific questions
   - **5 cards**: Balanced overview of a situation
   - **7 cards**: Comprehensive, general overview

2. **Enter Your Question**: Type your question or describe your situation in natural language
   - Examples:
     - "Will I find success in my new business venture?"
     - "What do I need to know about my relationship right now?"
     - "Guide me on my career path"
     - "I'm feeling lost and confused, what should I focus on?"

3. **Draw and Analyze**: Click the "✨ Light your path: Draw and Analyze the Cards" button

4. **View Results**: 
   - Card images (upside down if reversed)
   - Detailed interpretation for each card
   - Overall reading linking cards to your context
   - Mystical symbolism analysis
   - Psychological advice for improvement

### Example Scenarios

#### Example 1: Career Guidance
```
Select: 5 cards
Question: "I'm considering a major career change. Should I take the risk?"

Possible Reading:
- The cards might show courage, potential obstacles, and transformative change
- AI provides analysis considering your risk tolerance
- Psychological insights on decision-making
```

#### Example 2: Relationship Insight
```
Select: 3 cards
Question: "How can I improve my relationship with my partner?"

Possible Reading:
- Cards offer perspective on communication, emotions, and harmony
- Detailed interpretation of what each card means for relationships
- Advice based on both tarot wisdom and psychology
```

#### Example 3: General Life Direction
```
Select: 7 cards
Question: "Guide me on my spiritual journey this year"

Possible Reading:
- Comprehensive overview of challenges and opportunities
- Deep symbolic analysis
- Guidance for personal growth and transformation
```

## 📁 Project Structure

```
chat-with-tarots/
├── app.py                          # Main Streamlit application
├── requirements.txt                # Python dependencies
├── helpers/
│   ├── __pycache__/               # Python cache directory
│   └── help_func.py               # Helper functions for the LangChain chain
├── data/
│   ├── tarots.csv                 # 78 tarot cards with meanings and symbolism
│   └── readme/
│          └── system archietecture 1 .png  # System architecture diagram
│       
└── images/
    ├── 00-thefool.jpg             # Fool through World (22 Major Arcana)
    ├── 01-themagician.jpg
    ├── ...
    ├── 22-aceofwands.jpg          # Wands suit (14 cards)
    ├── ...
    ├── 36-aceofcups.jpg           # Cups suit (14 cards)
    ├── ...
    ├── 50-aceofswords.jpg         # Swords suit (14 cards)
    ├── ...
    └── 64-aceofpentacles.jpg      # Pentacles suit (14 cards)
```
### Key Components

#### 1. **app.py** - Main Application
- Loads CSV data into a knowledge base
- Sets up Streamlit UI with sidebar controls
- Implements the LangChain chain for analysis
- Displays card images and interpretations
- Handles user interactions

#### 2. **helpers/help_func.py** - Helper Functions

**Key Functions:**

- `generate_random_draw(num_cards, card_names_dataset)`
  - Randomly selects the specified number of cards
  - Randomly reverses ~50% of cards
  - Returns card info with orientation data

- `format_card_details_for_prompt(card_data, card_meanings)`
  - Formats selected cards and their meanings
  - Includes whether card is upright or reversed
  - Prepares text for LLM consumption

- `prepare_prompt_input(input_dict, meanings_dict)`
  - Extracts symbolism from selected cards
  - Combines card details with user context
  - Creates structured input for the prompt template

- `llm` (ChatOllama Configuration)
  - Initializes connection to local Ollama instance
  - Sets model to phi3:mini
  - Temperature: 0.9 (creative, varied responses)

#### 3. **data/tarots.csv** - Card Database

**Structure:**
```
card;upright;reversed;symbolism
[card-image.jpg];[upright meaning];[reversed meaning];[detailed symbolism description]
```

**Example:**
```
00-thefool.jpg;Beginnings, innocence, spontaneity...;Recklessness, carelessness, negligence...;The Fool is depicted as a young man...
```

Contains **78 cards**:
- **Major Arcana** (0-21): Life lessons and spiritual insights
- **Wands** (22-35): Passion, creativity, action
- **Cups** (36-49): Emotions, relationships, intuition
- **Swords** (50-63): Communication, conflict, intellect
- **Pentacles** (64-77): Work, money, material matters

#### 4. **Prompt Template**

The LLM receives a structured prompt that includes:
- **Card Details**: Names, orientations, and meanings
- **Context**: User's specific question or situation
- **Symbolism**: Deep symbolic meanings from the CSV
- **Instructions**: Guidelines for analysis and advice

```python
prompt_analysis = PromptTemplate.from_template("""
Analyze the following tarot cards, based on the meanings provided (also considering if they are reversed):
{card_details}
Pay attention to these aspects:
- Provide a detailed analysis of the meaning of each card (upright or reversed).
- Then offer a general interpretation of the answer based on the cards, linking it to the context: {context}.
- Be mystical and provide information on the interpretation related to the symbolism of the cards, based on the specific column: {symbolism}.
- At the end of the reading, always offer advice to improve or address the situation. Also, base it on your knowledge of psychology.
""")
```

## 🔗 LangChain Chain Explanation

The application uses **LangChain Expression Language (LCEL)** to create a sophisticated processing chain:

```python
analyzer = (
    RunnableParallel(
        cards=lambda x: x['cards'],
        context=lambda x: x['context']
    )
    | (lambda x: hf.prepare_prompt_input(x, card_meanings))
    | prompt_analysis
    | hf.llm
)
```

**Flow:**
1. **RunnableParallel**: Extracts cards and context from input
2. **prepare_prompt_input**: Formats data with meanings and symbolism
3. **prompt_analysis**: PromptTemplate structures the analysis request
4. **hf.llm**: Sends to Ollama for processing and returns interpretation

## 🎨 Visual Card Representation

### Card Display
- **Upright cards**: Displayed normally
- **Reversed cards**: Rotated 180 degrees for visual indication
- **Label format**: Card name + "(R)" for reversed

### Image Files
- Named after card names: `00-thefool.jpg`, `01-themagician.jpg`, etc.
- Located in `images/` directory
- Reference in CSV `card` column must match filename exactly

## ⚙️ Configuration & Customization

### Modify Number of Cards

In `app.py`, change the selectbox options:

```python
num_cards = st.selectbox("...", [3, 5, 7])  # Change this list
```

### Adjust LLM Model or Parameters

In `helpers/help_func.py`:

```python
llm = ChatOllama(
    base_url="http://localhost:11434",
    model="phi3:mini",  # Change model here
    temperature=0.9,     # 0.0-1.0: Lower = deterministic, Higher = creative
)
```

**Temperature Settings:**
- `0.0-0.3`: Focused, factual responses
- `0.5-0.7`: Balanced creativity
- `0.8-1.0`: Highly creative, unpredictable

### Use Different Ollama Models

```bash
ollama pull mistral          # Larger, more capable
ollama pull neural-chat      # Optimized for conversation
ollama pull dolphin-mixtral  # Advanced reasoning
```

### Customize Prompt Template

Edit the `prompt_analysis` template in `app.py` to change:
- Analysis style
- Emphasis on different aspects
- Output format
- Advice focus

## 📚 Understanding the Tarot Cards

### Card Categories

**Major Arcana (0-21): The Fool's Journey**
- Represents major life lessons and spiritual growth
- Examples: The Magician (Will), The High Priestess (Intuition), Death (Transformation)

**Minor Arcana - Wands (22-35): Fire, Action, Passion**
- Represents creativity, energy, passion, and action
- Numbered cards (Ace-10) + Court cards (Page-King)

**Minor Arcana - Cups (36-49): Water, Emotions, Relationships**
- Represents emotions, love, creativity, relationships
- Associated with the heart and feelings

**Minor Arcana - Swords (50-63): Air, Intellect, Communication**
- Represents communication, conflict, clarity, challenges
- Associated with the mind and thoughts

**Minor Arcana - Pentacles (64-77): Earth, Material, Work**
- Represents work, money, health, material matters
- Associated with physical reality and resources

### Upright vs. Reversed

- **Upright**: The card's direct, affirmative meaning
- **Reversed**: The opposite or shadow aspect, blocked energy, or internalized version

## 📊 Performance Optimization

### Memory Usage
- Model size: phi3:mini ~3.8GB
- App runtime: ~200-500MB
- Minimum total: 4-5GB

### Response Time
- Typical LLM response: 5-15 seconds
- Faster with better GPU
- Can be optimized with lower temperature

### Scaling Options
1. **Batch processing**: Create multiple readings programmatically
2. **Caching**: Store common card interpretations
3. **Parallel spreads**: Run multiple readings simultaneously

## 🤝 Contributing

To enhance this project:

1. **Add more cards**: Expand the tarot database with additional interpretations
2. **Improve symbolism**: Enhance card descriptions with artistic analysis
3. **New spreads**: Implement specialized reading types (Celtic Cross, etc.)
4. **Better UI**: Enhance visual design with custom CSS
5. **Database**: Migrate from CSV to database for better performance

## ⚖️ License

This project solely belongs to Jagrat Agrawal.

## 🌈 Final Notes

This application demonstrates the power of combining:
- **Ancient wisdom** (Tarot tradition)
- **Modern AI** (Large Language Models)
- **Web technology** (Streamlit)
- **Data processing** (Pandas, LangChain)

The result is a tool that provides meaningful guidance by blending symbolic interpretation with AI-powered analysis.

---

**Build by ❤️ Jagrat Agrawal ✨🔮✨**




