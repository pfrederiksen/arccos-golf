# Arccos Golf Performance Analyzer

A comprehensive OpenClaw skill for analyzing Arccos Golf sensor data including club distances, strokes gained metrics, scoring patterns, and performance trends.

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

## 📋 Data Requirements

The analyzer expects a JSON file with Arccos Golf data including:

- Golfer information and basic stats
- Strokes gained metrics by category
- Club distance and shot count data
- Scoring averages and distribution
- Putting performance metrics
- Recent round history

See [SKILL.md](SKILL.md) for complete data format specification.

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

**Note**: This analyzer processes pre-collected Arccos data. Data collection from the Arccos Golf platform requires separate browser automation tools and valid Arccos account credentials.