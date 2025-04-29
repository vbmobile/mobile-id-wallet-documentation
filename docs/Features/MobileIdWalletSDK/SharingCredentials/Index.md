# Sharing Credentials

Verifiable credentials (VCs) provide a secure, tamper-proof way to issue, share, and verify digital credentials. When sharing or presenting a credential, users can selectively disclose information based on the verifier's request. This means they can prove specific claims (e.g., age or membership) without exposing unrelated details. The process typically involves cryptographic proofs, ensuring authenticity while preventing forgery or unauthorized modifications. VCs also support privacy-preserving techniques like zero-knowledge proofs, allowing users to confirm a fact without revealing the underlying data. This makes credential sharing both secure and user-controlled across various digital interactions.

## Sharing credentials using Deep linking

=== "Android"

    ```kotlin
    launch {
		val result = MobileIdWallet.getInstance().sharePassportCredential(
			input = SharePassportCredential.Input(
				url = intent.data,
				verifiedCredentialId = verifiedCredentialId,
				requiresAuthenticationToCompleteFlow = true
			)
		)

		if (result.isSuccess && result.getOrNull()?.success == true) {
			// TODO handle success here
		} else {
			// TODO handle error here
		}
	}
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
	    /// Given a presentation request, will pick a random Verified Credential stored and share/present it
	    func handleWithoutUI(url: URL) {
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
	                // On return we will get all the activities associated to that credential
	                // Activities are events of 2 type: issuance (when credential is created)
	                // and present (when credential is presented)
	                print(output.activityForDocument.last ?? "")
	            } catch {
	                print(error)
	            }
	        }
	    }
	}
    ```

