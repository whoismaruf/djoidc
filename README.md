# Django OIDC Provider

A Django-based OpenID Connect (OIDC) provider implementation that allows you to create an OAuth 2.0 and OpenID Connect identity server.

## Overview

This project implements an OIDC provider using Django and the `django-oidc-provider` package. It provides authentication services that can be used by client applications to implement single sign-on (SSO) functionality.

## Features

- **OpenID Connect Provider**: Full OIDC server implementation
- **OAuth 2.0 Support**: Complete OAuth 2.0 authorization server
- **Django Integration**: Built on Django 5.2.6 with admin interface
- **SQLite Database**: Local development database
- **Custom Login Template**: Customizable authentication interface
- **Client Management**: Support for managing OIDC client applications

## Requirements

- Python 3.8+
- Django 5.2.6
- See `requirements.txt` for complete dependency list

## Installation

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd djoidc
   ```

2. **Create a virtual environment**
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Run database migrations**
   ```bash
   python manage.py migrate
   ```

5. **Create a superuser**
   ```bash
   python manage.py createsuperuser
   ```

6. **Start the development server**
   ```bash
   python manage.py runserver
   ```

## Configuration

### Environment Setup

For production deployment, ensure you:

1. **Change the SECRET_KEY** in `www/settings.py`
2. **Set DEBUG = False** for production
3. **Configure ALLOWED_HOSTS** appropriately
4. **Use a production database** (PostgreSQL, MySQL, etc.)

### OIDC Provider Configuration

The OIDC provider is configured in `www/settings.py`. Key configurations include:

- OIDC provider is included in `INSTALLED_APPS`
- Login URL is set to `/login/`
- Templates directory is configured for custom login page

## URLs and Endpoints

- **Admin Interface**: `/admin/` - Django admin for managing users and OIDC clients
- **Login**: `/login/` - User authentication endpoint
- **OIDC Endpoints**: `/openid/` - All OIDC-related endpoints including:
  - Authorization endpoint
  - Token endpoint
  - Userinfo endpoint
  - JWKS endpoint
  - Discovery endpoint (`.well-known/openid_configuration`)

## Client Application Setup

To register a client application:

1. Access the Django admin interface at `/admin/`
2. Navigate to the OIDC Provider section
3. Add a new Client with:
   - Client ID and Secret
   - Redirect URIs
   - Response types (code, token, id_token)
   - Grant types (authorization_code, implicit, refresh_token)
   - Scopes (openid, profile, email, etc.)

## Development

### Project Structure

```
djoidc/
├── db.sqlite3              # SQLite database
├── manage.py               # Django management script
├── requirements.txt        # Python dependencies
├── oidc_provider/          # OIDC provider data/clients
│   └── clients/            # Client-specific assets
├── templates/              # Custom templates
│   └── login.html          # Login page template
└── www/                    # Main Django project
    ├── __init__.py
    ├── asgi.py            # ASGI configuration
    ├── settings.py        # Django settings
    ├── urls.py            # URL routing
    └── wsgi.py            # WSGI configuration
```

### Running Tests

```bash
python manage.py test
```

### Collecting Static Files (for production)

```bash
python manage.py collectstatic
```

## Security Considerations

- Change the default `SECRET_KEY` before deploying to production
- Use HTTPS in production environments
- Properly configure CORS if needed for cross-origin requests
- Regularly update dependencies to patch security vulnerabilities
- Use strong passwords for admin accounts
- Configure proper backup strategies for user data

## OIDC Discovery

The OIDC discovery document is available at:
```
http://localhost:8000/openid/.well-known/openid_configuration
```

This provides client applications with all necessary endpoints and supported features.

## Troubleshooting

### Common Issues

1. **Migration errors**: Ensure all dependencies are installed and run `python manage.py migrate`
2. **Template not found**: Verify the `TEMPLATES` configuration in settings.py
3. **OIDC endpoints not working**: Check that `oidc_provider` is in `INSTALLED_APPS`

### Logs

Check Django logs for detailed error information. In development, errors are displayed in the browser when `DEBUG = True`.

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests if applicable
5. Submit a pull request

## License

[Add your license information here]

## Support

[Add support contact information or links to documentation]

---

For more information about django-oidc-provider, visit: https://github.com/juanifioren/django-oidc-provider