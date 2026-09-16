# Configuration Guide

## Configuration Methods

Shannon.ai can be configured in multiple ways:

1. **Python Code** - Direct configuration in code
2. **YAML File** - Configuration file (config.yaml)
3. **Environment Variables** - Via .env file

## Python Configuration

```python
from shannon import PenetrationTester
from shannon.utils.config import TargetConfig

config = TargetConfig(
    target_url="https://example.com",
    timeout=30,
    retries=3,
    concurrent_requests=5,
    verify_ssl=True,
)

tester = PenetrationTester(config)
```

## YAML Configuration

Create `config.yaml`:

```yaml
scanner:
  timeout: 30
  retries: 3
  concurrent_requests: 5
  verify_ssl: true

target:
  url: "https://example.com"
  api_endpoints:
    - "/api/v1/users"
    - "/api/v1/auth"
  
authentication:
  type: "bearer"
  token: "your-token-here"

payloads:
  enable_default: true
  custom_payloads_dir: "./custom_payloads"

reporting:
  format: "html"
  output_dir: "./reports"
```

## Configuration Options

### Scanner Options

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| timeout | int | 30 | Request timeout in seconds |
| retries | int | 3 | Number of retry attempts |
| concurrent_requests | int | 5 | Number of concurrent requests |
| verify_ssl | bool | true | Verify SSL certificates |

### Target Options

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| target_url | str | - | Target URL |
| api_endpoints | list | [] | API endpoints to test |
| include_source_code | bool | false | Include source code analysis |

### Authentication Options

| Type | Configuration |
|------|---------------|
| none | No authentication |
| basic | username/password |
| bearer | token |
| custom | Custom headers |

### Reporting Options

| Option | Description |
|--------|-------------|
| html | Generate HTML report |
| json | Generate JSON report |
| pdf | Generate PDF report |

## Environment Variables

Create `.env` file:

```env
SHANNON_TARGET_URL=https://example.com
SHANNON_TIMEOUT=30
SHANNON_RETRIES=3
SHANNON_AUTH_TYPE=bearer
SHANNON_AUTH_TOKEN=your-token
```

## Advanced Configuration

### Custom Payloads

Create a `custom_payloads.txt` file with one payload per line:

```
' OR '1'='1
admin' --
<script>alert('XSS')</script>
```

### Proxy Configuration

```python
config = TargetConfig(
    target_url="https://example.com",
    proxy="http://proxy.example.com:8080"
)
```

### Custom Headers

```python
config = TargetConfig(
    target_url="https://example.com",
    custom_headers={
        "X-API-Key": "your-api-key",
        "Authorization": "Bearer token",
    }
)
```
