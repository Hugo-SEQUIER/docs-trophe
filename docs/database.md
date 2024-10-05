---
sidebar_position: 3
title: "Database"
hidden: false
---

# Database

## Irys: A Programmable Datachain

Irys is the first Layer 1 (L1) programmable datachain designed to optimize both data storage and execution. By integrating storage and execution, Irys enhances the utility of blockspace, enabling a broader spectrum of web services to operate on-chain-services that are currently not feasible.

### Key Features of Irys

- **Unified Platform:** Combines data storage and execution, allowing developers to eliminate dependencies and integrate efficient on-chain data seamlessly.
- **Cost-Effective Storage:** Optimized specifically for data storage, making it significantly cheaper to store data on-chain compared to traditional blockchains focused on smart contracts and financial applications.
- **Programmable Datachain:** The IrysVM can utilize on-chain data during computations, enabling dynamic and real-time applications within a single platform.
- **Decentralization:** Designed to minimize centralization risks by distributing control, enhancing the security and trustworthiness of the network.
- **Free Storage for Small Data:** Storing less than 100KB of data is free, making it accessible for small-scale applications and metadata storage.
- **GraphQL Querying:** Metadata stored on Irys can be queried using GraphQL, providing a flexible and efficient way to retrieve on-chain data.

### Key Management

To store data on Irys, a private key is required. At Trophē, we employ a user-centric approach to key management that prioritizes security and user control:

1. **User Secret Generation:** When a user creates a new account, we generate a unique keypair for them. The public key is stored in our database, associated with the user's account.

2. **Private Key Handling:** The private key is never stored on our servers. Instead, it's managed client-side using the following approach:

   a. **Initial Key Provision:** Upon account creation or first login, the user is provided with their private key and instructed to store it securely offline (e.g., in a password manager or secure physical location).
   
   b. **Session-based Key Usage:** When the user logs in, they are prompted to enter their private key in a secure input field. This key is then:
      - Stored in the browser's memory (JavaScript runtime) for the duration of the session.
      - Never sent to the server or stored in persistent browser storage (cookies, localStorage, etc.).
      - Cleared from memory when the user logs out or the session expires.

   c. **Key Input Security:** To enhance security during key input, we implement several measures:
      - Custom Input Field: We utilize a specially designed input field that masks the private key, preventing it from being visible on the screen.
      - Encrypted Communication: All communication between the client and our servers is encrypted using HTTPS. This ensures that the private key and other sensitive data remain secure during transmission.

   These security measures work together to provide a robust defense against various attack vectors, helping to keep our users' private keys safe and secure.

3. **Data Encryption and Decryption:** 
   - Encryption: Data is encrypted using the public key associated with the user's account. This can be done on either the client-side or server-side, as the public key is not sensitive information.
   - Decryption: Decryption occurs exclusively on the client-side using the private key stored in memory. Only the owner of the private key can decrypt the data, ensuring that sensitive information remains protected even if intercepted during transmission or storage.

4. **Key Recovery:**
   To ensure users can recover their private keys in case of loss, we implement a secure key recovery mechanism:
   - During account creation, we generate a recovery phrase (mnemonic) from the private key.
   - This mnemonic is presented to the user with clear instructions to store it securely offline.
   - Users are strongly advised to write down the mnemonic and keep it in a safe place, separate from their usual digital storage.
   - The mnemonic is never stored on our servers, maintaining the user's sole control over their private key.

5. **Session Management:**
   To enhance security during active sessions, we implement the following measures:
   - Secure session timeouts: After a period of inactivity, the session automatically expires, requiring re-authentication.
   - Clear logout functionality: A prominent logout button is provided, which, when clicked, immediately wipes the private key from memory.
   - Automatic logout: When the user closes the tab or exits the browser, the session is terminated, and the private key is cleared from memory.

These security features work in tandem to protect user private keys and minimize the risk of unauthorized access.

### Retrieving Metadata

Irys provides a powerful GraphQL API for querying transaction metadata. This allows you to efficiently retrieve and filter data stored on the Irys network. Here's a comprehensive guide on how to use this feature:

#### GraphQL Query Structure

The basic structure of a GraphQL query to retrieve metadata looks like this:

```graphql
query getByOwner($appPrivateKey: String!, $userPublicKey: String!) {
    transactions(
        owners: [$appPrivateKey], 
        tags: [{name: "address", values: [$userPublicKey]}]
    ) {
        edges {
            node {
                id
            }
        }
    }
}
```

This query does the following:
- Filters transactions by the `appPrivateKey` (owner of the transaction)
- Further filters by a tag with the name "address" and the value of `userPublicKey`
- Retrieves the transaction ID

#### Retrieving Transaction Data

Once you have the transaction IDs, you can retrieve the actual data using the Irys gateway:

```javascript
const transactionId = data.transactions.edges[0].node.id;
const dataUrl = `https://gateway.irys.xyz/${transactionId}`;

const response = await fetch(dataUrl);
const transactionData = await response.json();
```

By leveraging these querying capabilities, we can efficiently retrieve and manage data stored on the Irys network, enabling powerful and flexible data management in our application.

## Supabase: Open-Source Database Solution

Supabase is an open-source database platform that offers robust authentication and user management capabilities. It serves as the backbone for managing user data and authentication processes, ensuring secure and efficient handling of user information.

### Key Features of Supabase

- **Authentication:** Provides comprehensive authentication services, including support for various authentication methods and secure user management.
- **Real-Time Database:** Enables real-time data synchronization, allowing applications to respond instantly to data changes.
- **Scalability:** Designed to scale with your application, handling increasing loads without compromising performance.
- **Open-Source:** Offers transparency and flexibility, allowing developers to customize and extend functionality as needed.

## Integration of Irys and Supabase

At Trophē, we leverage both Irys and Supabase to create a powerful and secure platform:

- **Metadata Storage with Irys:** We use Irys to store metadata on the blockchain, benefiting from its cost-effective and programmable datachain capabilities. This ensures that metadata is securely stored and easily accessible for on-chain applications. Each user is assigned a keypair upon account creation, facilitating the storage and retrieval of metadata. Storing less than 100KB of data is free, and metadata can be queried using GraphQL.
- **Authentication and User Information with Supabase:** Supabase handles authentication and manages user information, providing a reliable and scalable solution for securing user data and managing access control.

By integrating Irys and Supabase, we combine the strengths of blockchain-based data storage with modern authentication solutions, delivering a seamless and secure user experience.

## Conclusion

Our database strategy utilizes Irys for efficient and programmable on-chain metadata storage and Supabase for robust authentication and user management. This combination ensures that our platform is both secure and scalable, capable of supporting innovative applications and providing a solid foundation for future growth.

