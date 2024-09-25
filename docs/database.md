---
sidebar_position: 3
title: "Database"
hidden: false
---

# Database

## Irys: A Programmable Datachain

Irys is the first Layer 1 (L1) programmable datachain designed to optimize both data storage and execution. By integrating storage and execution, Irys enhances the utility of blockspace, enabling a broader spectrum of web services to operate on-chain—services that are currently not feasible.

### Key Features of Irys

- **Unified Platform:** Combines data storage and execution, allowing developers to eliminate dependencies and integrate efficient on-chain data seamlessly.
- **Cost-Effective Storage:** Optimized specifically for data storage, making it significantly cheaper to store data on-chain compared to traditional blockchains focused on smart contracts and financial applications.
- **Programmable Datachain:** The IrysVM can utilize on-chain data during computations, enabling dynamic and real-time applications within a single platform.
- **Decentralization:** Designed to minimize centralization risks by distributing control, enhancing the security and trustworthiness of the network.
- **Free Storage for Small Data:** Storing less than 100KB of data is free, making it accessible for small-scale applications and metadata storage.
- **GraphQL Querying:** Metadata stored on Irys can be queried using GraphQL, providing a flexible and efficient way to retrieve on-chain data.

### Key Management

To store data on Irys, an Ethereum (ETH) private key is required. When a user creates a new account, a keypair is assigned to them. This keypair simplifies the process of storing and retrieving metadata on the Irys blockchain.

### Retrieving Metadata

You can query Irys transaction metadata using GraphQL. Here is an example query to retrieve metadata:

```graphql
query getIDsForWallet {
    transactions(
        owners: ["0xbe9c3578964c0fb32da4de76b73d5d289d0f54c4"] # Query argument
        order: ASC
    ) {
        edges {
            node {
                id  # Result field
            }
        }
    }
}
```

## Supabase: Open-Source Database Solution

Supabase is an open-source database platform that offers robust authentication and user management capabilities. It serves as the backbone for managing user data and authentication processes, ensuring secure and efficient handling of user information.

### Key Features of Supabase

- **Authentication:** Provides comprehensive authentication services, including support for various authentication methods and secure user management.
- **Real-Time Database:** Enables real-time data synchronization, allowing applications to respond instantly to data changes.
- **Scalability:** Designed to scale with your application, handling increasing loads without compromising performance.
- **Open-Source:** Offers transparency and flexibility, allowing developers to customize and extend functionality as needed.

## Integration of Irys and Supabase

At Trophe, we leverage both Irys and Supabase to create a powerful and secure platform:

- **Metadata Storage with Irys:** We use Irys to store metadata on the blockchain, benefiting from its cost-effective and programmable datachain capabilities. This ensures that metadata is securely stored and easily accessible for on-chain applications. Each user is assigned a keypair upon account creation, facilitating the storage and retrieval of metadata. Storing less than 100KB of data is free, and metadata can be queried using GraphQL.
- **Authentication and User Information with Supabase:** Supabase handles authentication and manages user information, providing a reliable and scalable solution for securing user data and managing access control.

By integrating Irys and Supabase, we combine the strengths of blockchain-based data storage with modern authentication solutions, delivering a seamless and secure user experience.

## Conclusion

Our database strategy utilizes Irys for efficient and programmable on-chain metadata storage and Supabase for robust authentication and user management. This combination ensures that our platform is both secure and scalable, capable of supporting innovative applications and providing a solid foundation for future growth.

