# Arccos Golf Performance Analyzer

A comprehensive OpenClaw skill for analyzing Arccos Golf sensor data including club distances, strokes gained metrics, scoring patterns, and performance trends. **Analysis only** - reads local JSON file, no network access or credential handling. Data collection requires separate browser automation (see privacy notes below).

## 🏌️ Features

- **Strokes Gained Analysis**: Compare your performance to PGA Tour averages across all game categories
- **Club Distance Tracking**: Analyze average distances, shot counts, and consistency for each club
- **Scoring Patterns**: Understand your performance on different par values and score distribution
- **Putting Performance**: Track putts per round, GIR putting, and distance-based metrics
- **Approach Shot Analysis**: Analyze greens in regulation, miss patterns, and terrain performance
- **Round Tracking**: Monitor recent performance trends and course-specific analysis
- **Multiple Output Formats**: Human-readable reports and machine-readable JSON

## 🚀 Quick Start

### Installation

```bash
# Via ClawHub
clawhub install arccos-golf

# Or clone this repository
git clone https://github.com/pfrederiksen/arccos-golf.git
cd arccos-golf
```

### Basic Usage

```bash
# Full performance report
python3 scripts/arccos_golf.py data/arccos-data.json

# Summary statistics only
python3 scripts/arccos_golf.py data/arccos-data.json --summary

# Strokes gained analysis
python3 scripts/arccos_golf.py data/arccos-data.json --strokes-gained

# Club distance analysis
python3 scripts/arccos_golf.py data/arccos-data.json --clubs iron

# JSON output for further processing
python3 scripts/arccos_golf.py data/arccos-data.json --format json
```

## 📊 Example Output

```
🏌️ Arccos Golf Performance Report
========================================
Golfer: Paul Frederiksen
Total Shots Tracked: 7,057
Total Rounds: 75
Longest Drive: 308 yards

📊 STROKES GAINED ANALYSIS
------------------------------
Overall: -12.0
Approach: -5.0
Driving: -3.3
Short Game: -2.7
Putting: -1.1

🎯 Priority Areas:
  1. Approach
  2. Driving  
  3. Short Game

🏌️ CLUB DISTANCES
--------------------
Driver: 234 yds avg (533 shots, longest: 281)
3 Wood: 204 yds avg (57 shots, longest: 320)
7 Iron: 140 yds avg (43 shots, longest: 168)
```

## 📋 Getting Your Arccos Data

⚠️ **PRIVACY NOTICE**: The following data collection guide involves browser automation with cloud services and credential transmission. Consider privacy implications before proceeding.

Arccos Golf does not offer a public API, so data must be scraped from **https://dashboard.arccosgolf.com** using browser automation.

### Recommended: browser-use (Privacy Considerations)

**⚠️ External Services Involved:**
- **Cloud browser service** (browser-use API) - receives your Arccos login credentials
- **LLM provider** (OpenAI/Anthropic via ChatBrowserUse) - processes golf data and credentials  
- **Arccos dashboard** - accessed via cloud browser with your credentials

**Alternative**: For maximum privacy, manually export your Arccos data and create the JSON file locally.

[browser-use](https://github.com/browser-use/browser-use) is an AI-powered browser automation library that can navigate the Arccos dashboard and extract your stats.

```bash
pip install browser-use langchain-openai
```

```python
import asyncio
from browser_use import Agent, Browser, ChatBrowserUse

async def main():
    # WARNING: This sends your Arccos credentials to cloud services
    browser = Browser(use_cloud=True)  # Cloud browser service
    llm = ChatBrowserUse()  # Requires OpenAI API key
    agent = Agent(
        task="""Log into https://dashboard.arccosgolf.com/login with my credentials.
        Extract all stats: Strokes Gained, club distances, scoring, GIR,
        driving accuracy, putting, short game, and recent rounds.
        Save as JSON to arccos-data.json""",
        llm=llm, browser=browser,
    )
    await agent.run(max_steps=60)

asyncio.run(main())
```

**Credentials Required:**
- Arccos login credentials (transmitted to cloud browser)  
- OpenAI API key (for ChatBrowserUse LLM)
- browser-use cloud service access

### What to scrape

The Arccos dashboard has two versions — scrape both for complete data:

| Section | Dashboard | Data |
|---------|-----------|------|
| SG Breakdown | New (`/stats/overall`) | Driving, Approach, Short, Putting |
| Driving | New (`/stats/driving`) | Fairways %, distance, SG by hole length |
| Approach | New (`/stats/approach`) | GIR %, miss patterns, SG by distance |
| Short Game | New (`/stats/short`) | Up & Down %, sand saves |
| Putting | New (`/stats/putting`) | Putts/hole, SG by putt length |
| Scoring Mix | v1 (`/overall performance`) | Birdie/par/bogey/double+ % |
| Club Distances | v1 (`/clubs` → Distance) | Avg distance per club |
| Round History | v1 (`/rounds`) | Scores + per-category breakdown |

See [SKILL.md](SKILL.md) for the complete expected JSON format.

**Privacy Reminder:** The above method transmits your Arccos credentials and golf performance data to cloud services. For sensitive data, consider manual data export instead.

## 🔒 Security & Privacy

This skill is designed with security in mind:

- ✅ **Read-only**: Only reads provided data files, never modifies anything
- ✅ **No network access**: All processing done locally
- ✅ **No subprocess calls**: Uses only Python standard library
- ✅ **No credentials**: Does not handle or store authentication data
- ✅ **Standard library only**: No external dependencies

Data collection from Arccos must be performed separately using browser automation tools.

## 📖 Available Commands

| Command | Description |
|---------|-------------|
| `--summary` | Show basic statistics summary |
| `--strokes-gained` | Analyze strokes gained performance |
| `--clubs [type]` | Show club distances (optionally filtered) |
| `--format json` | Output as JSON instead of text |
| `--recent-rounds N` | Show N most recent rounds |

## 🎯 Golf Metrics Explained

### Strokes Gained
Measures your performance relative to PGA Tour averages:
- **Positive values**: Better than tour average
- **Negative values**: Worse than tour average
- **Overall**: Combined performance across all categories

### Categories
- **Driving**: Tee shots to landing position
- **Approach**: Shots to the green from fairway/rough
- **Short Game**: Chipping and pitching around the green
- **Putting**: Performance on the green

## 🤝 Contributing

Contributions welcome! Please feel free to submit issues or pull requests.

## 📄 License

This project is open source and available under the MIT License.

## 🔗 Related Projects

- [OpenClaw](https://github.com/openclaw/openclaw) - AI-powered CLI assistant
- [GHIN Golf Tracker](https://github.com/pfrederiksen/ghin-golf-tracker) - GHIN handicap analysis skill

---

**Note**: This skill analyzes pre-collected Arccos data. See the [Data Collection Guide](#-getting-your-arccos-data) above for how to scrape your stats from `dashboard.arccosgolf.com` using browser-use.