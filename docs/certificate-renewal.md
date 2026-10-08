# Certificate Renewal

AWS Certificate Manager (ACM) manages the public SSL/TLS certificate.

The certificate uses DNS validation.

The ACM validation CNAME record should remain in the DNS configuration so that ACM can continue to validate the domain for automatic renewal.

If certificate renewal fails and the certificate expires, HTTPS connections can show certificate errors and secure access may become unavailable.

Therefore:

- Keep the ACM validation CNAME record.
- Do not remove the DNS validation record.
- Monitor the ACM certificate status.
