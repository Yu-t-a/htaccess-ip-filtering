# htaccess-ip-filtering

This project demonstrates how to use Apache's `.htaccess` file with mod_rewrite to control access to your website based on IP address and referer.

### Features:
- **IP-based Access Control**: Restrict access to specific IP addresses (e.g., only allowing localhost).
- **Referer-based Filtering**: Ensure that traffic is coming from a trusted domain (e.g., only allow requests from `Domain`).
- **Custom 403 Page**: Redirect unauthorized users to a custom 403 Forbidden page.

---

## Setup

1. **Prerequisites**: 
    - Apache server with `mod_rewrite` enabled.
    - Access to the `.htaccess` file of your website or directory.

2. **How to Use**:
    - Place the following code in your `.htaccess` file in the root directory of your website:

    ```apache
    <IfModule mod_rewrite.c>
        RewriteEngine On

        # Allow localhost
        RewriteCond %{REMOTE_ADDR} !^127\.0\.0\.1$
        
        # Allow traffic from Domain
        # RewriteCond %{HTTP_REFERER} !^https?://(www\.)?example\.go\.th [NC]
        RewriteCond %{HTTP_REFERER} !^https?://(www\.)?example\.com [NC]


        # Redirect all other requests to 403.html
        RewriteRule ^.*$ /403.html [L]
    </IfModule>
    ```

    - This configuration will:
        - Allow access from the localhost (`127.0.0.1`).
        - Allow requests originating from `Domain`.
        - Redirect all other unauthorized requests to a custom `403.html` page.

3. **Customizing the 403 Page**:
    - Create a `403.html` page that will be shown when access is denied.
    - You can place this file in the root directory or wherever you prefer.

---

## Benefits:
- **Improved Security**: Only allows traffic from trusted sources and blocks unauthorized access.
- **Prevent Hotlinking**: Restricts access to prevent unwanted traffic or hotlinking from other websites.
- **Customizable**: Easily adjust the allowed IP addresses and referer domains based on your needs.

---

