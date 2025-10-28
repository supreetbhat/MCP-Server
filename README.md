# Weather MCP Server

An MCP (Model Context Protocol) server for weather data that provides access to current weather alerts and forecasts from the US National Weather Service (NWS).

## Features

- 🌩️ **Weather Alerts**: Retrieves active weather alerts for US states
- 🌤️ **Weather Forecasts**: Provides detailed forecasts for any location (coordinates)
- 🔄 **Asynchronous API**: Uses modern async/await patterns for efficient requests
- ⚡ **FastMCP**: Built on the FastMCP framework for simple MCP server development

## Installation

### Prerequisites

- Python 3.10 or higher
- `pip` package manager

### Install Dependencies

bash

```bash
pip install httpx mcp
```

Or using a `requirements.txt`:

bash

```bash
pip install -r requirements.txt
```

**requirements.txt:**

```
httpx>=0.24.0
mcp>=0.1.0
```

## Usage

### Starting the Server

bash

```bash
python weather_server.py
```

The server runs in stdio transport mode and communicates via standard input/output.

### Available Tools

#### 1. get_alerts

Retrieves active weather alerts for a US state.

**Parameters:**

- `state` (string): Two-letter US state code (e.g., "CA", "NY", "TX")

**Example:**

python

```python
await get_alerts(state="CA")
```

**Returns:** Formatted alerts with event type, affected area, severity, description, and instructions.

#### 2. get_forecast

Retrieves the weather forecast for a specific location.

**Parameters:**

- `latitude` (float): Latitude of the location
- `longitude` (float): Longitude of the location

**Example:**

python

```python
await get_forecast(latitude=39.7456, longitude=-97.0892)
```

**Returns:** Detailed 5-period forecast with temperature, wind, and detailed description.

## API Details

### National Weather Service API

This server uses the official [NWS API](https://www.weather.gov/documentation/services-web-api):

- **Base URL**: `https://api.weather.gov`
- **Authentication**: None required
- **Rate Limiting**: Please observe NWS API usage guidelines
- **User-Agent**: Required (automatically set)

### Error Handling

The server implements robust error handling:

- Automatic timeouts (30 seconds)
- Graceful degradation on API errors
- Clear error messages for users

## Project Structure

```
weather-mcp-server/
├── weather_server.py    # Main server file
├── requirements.txt     # Python dependencies
└── README.md           # This file
```

## Development

### Code Style

The code follows modern Python conventions:

- Type hints for better IDE support
- Async/await for non-blocking I/O
- Clear function and variable names

### Extensions

To add new tools:

1. Define a new async function
2. Decorate it with `@mcp.tool()`
3. Add a clear docstring description
4. Implement the logic using `make_nws_request()`

**Example:**

python

```python
@mcp.tool()
async def get_radar(station_id: str) -> str:
    """Get radar data for a weather station.
    
    Args:
        station_id: NWS station identifier
    """
    # Implementation here
    pass
```

## Limitations

- Only available for US locations (NWS API)
- Requires internet connection
- Dependent on NWS API availability

## License

[Insert your license here - e.g., MIT, Apache 2.0, etc.]

## Contributing

Contributions are welcome! Please:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## Support

For questions or issues, please open an issue in the GitHub repository.

## Acknowledgments

- [National Weather Service](https://www.weather.gov/) for providing the free API
- [FastMCP](https://github.com/jlowin/fastmcp) for the MCP framework
- [httpx](https://www.python-httpx.org/) for the async HTTP client library