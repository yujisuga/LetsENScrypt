# Let's ENScrypt
A service that issues X.509 certificates for ENS-based domains

# Objectives
We considered a service that issues X.509 certificates for ENS-based domains.
When deploying a key to a Web server, it is assumed that ETH signing keys will be used, and we have considered a world where Web servers can be accessed via the ENS domain in the future.

# Base case
Let's Encrypt is already used for implementation as a free DV (Domain Validation) certificate issuance service.
We investigated a mechanism that can issue this to ENS-based domain names.

# In the near future
A world where Web services are provided using ENS domains just like .onion domains will work on the closed networks using Tor.
We imagined a future where E2EE communication is realized by implementing HTTP/HTTPS servers by extending the function of the Wallet.

# Deployment
In that case, it is assumed that the TLS secure protocol with encryption and authentication functions like HTTPS will be used, so it is necessary to consider how the certificate issuance service for ENS domain names, as well as the DV certificate issuance service.

# A challenge
The signing keys corresponding to the ETH addressed need to be deployed on the internet (just like a hot wallet)
Since this is very dangerous, we thought that it was necessary to set up a separate ENS subdomain FQDN.

# Solution
- Specifically, assuming that www.ee-global.eth can be a reverse lookup for ee-global.eth.
We concluded that it would be appropriate to issue an intermediate certificate and an EE certificate separately like a PKI certificate chain.
- Temporarily DNS (not ENS) service with ENS domain as a subdomain, such as www.ee-global.eth by enabling reverse lookups from the Internet for sub-subdomains of deploy-ens-to-dns.com.
www.ee-global.deploy-ens-to-dns.com can provide web services like the hosting service in this case)

# Benefits
Transfer of ETH, that is, by attaching a request (a normal DER format Certificate Signing Request can be used) along with the issuance fee payment, it can be completed with a simple 1-way protocol.
Since CSR is public information (for example, the same idea as Certificate Transparency), there are few security issues (however, discussion from the viewpoint of privacy protection is necessary)

# References
- OpenSSL commands
  https://www.openssl.org/docs/manmaster/man1/
- ERC-137: Ethereum Domain Name Service - Specification
  https://eips.ethereum.org/EIPS/eip-137
- ERC-5298: ENS Trust to hold NFTs under ENS name
  https://eips.ethereum.org/EIPS/eip-5298
- Let's Encrypt documents
  https://letsencrypt.org/docs/
- IETF RFC5280: Internet X.509 Public Key Infrastructure Certificate and CRL Profile
  https://www.rfc-editor.org/rfc/rfc5280
