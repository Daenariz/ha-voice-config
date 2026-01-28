# Home Assistant Voice Configuration

This repository contains the configuration files for a custom LLM-powered voice assistant for Home Assistant. It defines how the AI perceives the smart home and which actions it can perform.

## Components

### 1. `prompt.md` (System Prompt)
The system prompt defines the AI's personality and instructions:
- **Identity**: A knowledgeable "Smart Home Manager" with extensive expertise in music and general facts.
- **Rules**:
  - Responds in polite and concise language.
  - Direct execution: Does not talk about what it *might* do, but executes commands immediately.
  - Handles device states (exposed entities) and timestamps in a human-readable 12hr format.
  - Asks for missing information if a command is ambiguous.

### 2. `functions.yml` (Tool Definitions)
This file defines the technical "tools" or functions the AI can trigger:

- **`execute_services`**: The primary tool for controlling devices. It can target specific `entity_id` or entire `area_id` groups (e.g., "Turn off all lights in the living room").
- **`get_attributes`**: Allows the AI to look up detailed state information for any entity using a Jinja2 template.
- **`play_music`**: A specialized script integration to play music (artists, albums, or genres) on Music Assistant (MASS) satellite speakers.

## Integration

To use these files in Home Assistant:
1. Ensure you have the **OpenAI conversation** or a similar LLM integration installed.
2. Use the content of `prompt.md` as the System Prompt in your conversation agent settings.
3. Import or copy the functions from `functions.yml` into your LLM configuration to give the model "tool use" capabilities.

## Requirements

- **Home Assistant**
- **Exposed Entities**: Ensure the entities you want to control are exposed to the conversation agent.
- **Scripts**: The `play_music` function requires a matching script named `script.play_music` in your Home Assistant setup.
