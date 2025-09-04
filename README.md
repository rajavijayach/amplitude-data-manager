# Amplitude Data Manager

A comprehensive web-based tool for managing your Amplitude data. Upload CSV files to update user properties or send events directly to your Amplitude project using their APIs.

## ✨ Features

### 🏷️ **User Properties Tab**
- Update user identities and properties via Amplitude Identify API
- Batch processing of user data (1000 users per batch)
- Real-time progress tracking with detailed logging

### � **Events Tab**
- Send custom events with properties via Amplitude HTTP v2 API
- Support for event properties, timestamps, and session tracking
- Flexible CSV structure with automatic property mapping

### � **Security & Usability**
- Client-side processing - API keys never stored
- Data preview before sending to Amplitude
- Sample CSV downloads for both use cases
- Comprehensive error handling and validation
- Interactive tooltips and collapsible help guides

## 🚀 Getting Started

### Prerequisites
- A valid Amplitude project with API access
- CSV file with your data (format depends on your use case)

### Quick Start
1. **Open the Application**: Simply open `index.html` in any modern web browser
2. **Choose your tab**: User Properties or Events
3. **Enter API Key**: Get it from Amplitude Settings → Projects → [Your Project] → General
4. **Upload CSV**: Follow the format guide for your chosen feature
5. **Preview & Send**: Review your data and send to Amplitude

## 📋 CSV Formats

### User Properties CSV
Update user attributes and properties:

```csv
user_id,age,gender,subscription_type,last_login
user123@example.com,30,male,premium,2024-01-15
user456@example.com,25,female,free,2024-01-14
```

**Requirements:**
- Header row required
- `user_id` column mandatory
- Additional columns become user properties

### Events CSV
Send custom events with properties:

```csv
event_type,user_id,product_id,product_name,price,category,time,session_id
Product Viewed,user123,sku_123,Noise Cancelling Headphones,199.99,Electronics,1640995200000,1640995200000
Button Click,user456,,,,,1640995260000,1640995200000
Purchase,user123,sku_123,Noise Cancelling Headphones,199.99,Electronics,1640995320000,1640995200000
```

**Requirements:**
- Header row required
- `event_type` column mandatory
- Either `user_id` or `device_id` required
- Optional: `time` (milliseconds since epoch), `session_id`
- Additional columns become event properties

## 🔌 API Integration

### User Properties
Uses [Amplitude Identify API](https://amplitude.com/docs/apis/analytics/identify):
- **Endpoint**: `https://api2.amplitude.com/identify`
- **Method**: POST (form-urlencoded)
- **Batch limit**: 1000 users per request

### Events
Uses [Amplitude HTTP v2 API](https://amplitude.com/docs/apis/analytics/http-v2):
- **Endpoint**: `https://api2.amplitude.com/2/httpapi`
- **Method**: POST (JSON)
- **Batch limit**: 1000 events per request

## 🛠️ Technical Details

### Built With
- **HTML5** - Structure and semantic markup
- **Tailwind CSS** - Modern responsive styling
- **Vanilla JavaScript** - Core functionality and API integration
- **Fetch API** - HTTP requests to Amplitude

### Browser Compatibility
- ✅ Chrome (recommended)
- ✅ Firefox
- ✅ Safari
- ✅ Edge
- ✅ Any modern browser with ES6+ support

### Data Processing
- **Client-side only**: No data sent to any server except Amplitude
- **Automatic type conversion**: Numbers and booleans detected automatically
- **Batch processing**: Large files handled efficiently
- **Error recovery**: Retry logic for failed batches

## 🔒 Security

- **API keys**: Handled client-side only, never stored or logged
- **HTTPS**: All API calls use secure connections
- **No external dependencies**: Self-contained HTML file
- **Privacy**: No analytics or tracking beyond Amplitude APIs

## ⚠️ Error Handling & Troubleshooting

### Common Issues

| Issue | Solution |
|-------|----------|
| "Missing required column" | Ensure CSV has `user_id` (properties) or `event_type` + (`user_id` or `device_id`) (events) |
| "Invalid API Key" | Verify key from Amplitude Settings → Projects → General |
| "Rate limiting (429)" | Tool automatically retries after 30 seconds |
| "Network error" | Check internet connection and Amplitude status |
| "Batch failed" | Check API key validity and data format |

### Rate Limits
- **User Properties**: 1800 updates per hour per user
- **Events**: 30 events per second per user/device
- **Payload size**: Max 1MB per request


## 📚 Advanced Usage

### Event Properties Mapping
The tool automatically maps CSV columns to Amplitude event structure:

```javascript
// CSV Row: Product Viewed,user123,sku_123,Headphones,199.99,Electronics
// Becomes:
{
  "event_type": "Product Viewed",
  "user_id": "user123", 
  "event_properties": {
    "product_id": "sku_123",
    "product_name": "Headphones",
    "price": 199.99,
    "category": "Electronics"
  }
}
```

### Timestamp Handling
- Provide `time` column with milliseconds since epoch
- Omit for current timestamp
- Format: `1640995200000` (JavaScript `Date.now()` format)

## 🤝 Contributing

Contributions welcome! This project uses:
- Single HTML file architecture for simplicity
- Inline CSS and JavaScript for portability
- No build process or dependencies

To contribute:
1. Fork the repository
2. Make changes to `index.html`
3. Test with sample data
4. Submit pull request

## 📄 License

MIT License - feel free to use, modify, and distribute.

## 🙋‍♂️ Support

- **Documentation**: Comprehensive tooltips and help guides built-in
- **Issues**: Use GitHub Issues for bug reports and feature requests
- **Community**: Built for the Amplitude community

---

**Made with ❤️ for the Amplitude community**

