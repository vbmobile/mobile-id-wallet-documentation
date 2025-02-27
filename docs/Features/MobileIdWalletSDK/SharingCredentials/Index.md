# Sharing Credentials

Verifiable credentials (VCs) provide a secure, tamper-proof way to issue, share, and verify digital credentials. When sharing or presenting a credential, users can selectively disclose information based on the verifier's request. This means they can prove specific claims (e.g., age or membership) without exposing unrelated details. The process typically involves cryptographic proofs, ensuring authenticity while preventing forgery or unauthorized modifications. VCs also support privacy-preserving techniques like zero-knowledge proofs, allowing users to confirm a fact without revealing the underlying data. This makes credential sharing both secure and user-controlled across various digital interactions.

## Sharing credentials using Deep linking

=== "Android"

    ```kotlin
        ...
    ```

=== "iOS"

    ```swift
	import MobileIdWalletSDK
	import Foundation
	
	class DeeplinkManager {
	    let mobileIdWallet: MobileIdWalletProtocol
	    init(mobileIdWallet: MobileIdWalletProtocol) {
	        self.mobileIdWallet = mobileIdWallet
	    }
	}
	
	extension DeeplinkManager {
	    func handle(url: URL) {
	        Task {
	            // Step 1 - Validate URL
	            guard let scheme = url.scheme, scheme == "openid-vc" else {
	                // Invalid URL
	                return
	            }
	            do {
	                // Step 2 - Choose Credential to share
	                let fetchAllCredentialsOutput = try await mobileIdWallet.fetchAllCredentials(.init())
	                guard let credentialToShared = fetchAllCredentialsOutput.records.randomElement() else {
	                    // No credentias to share
	                    return
	                }
	                // Step 3 - Share Credential
	                let output = try await mobileIdWallet.shareCredential(.init(
	                    url: url.absoluteString,
	                    credentialId: credentialToShared.id,
	                    requiresAuthenticationToCompleteFlow: true
	                ))
	                print(output.activityForDocument.last ?? "")
	            } catch {
	                print(error)
	            }
	        }
	    }
	}
    ```

