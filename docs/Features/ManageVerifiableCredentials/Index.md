# Verifiable Credential 

This SDK provides a simple and flexible way to manage Verifiable Credentials, supporting full CRUD (Create, Read, Update, Delete) functionality. Whether you're issuing new credentials, retrieving stored ones, updating their contents, or securely deleting them, the SDK ensures a seamless integration experience.

Every function is available in both async/await and completion handler variants, allowing you to choose the approach that best suits your app's architecture. With a focus on performance and security, these operations help you manage credentials efficiently while keeping your implementation clean and maintainable.

## Fetch Verifiable Credentials

=== "Android"

    ```kotlin
        ...
    ```

=== "iOS"

    ```swift
	class ManageCredentials {
	    let mobileIdWallet: MobileIdWalletProtocol
	    init(mobileIdWallet: MobileIdWalletProtocol) {
	        self.mobileIdWallet = mobileIdWallet
	    }
	}
	
	extension ManageCredentials {
	    func fetchAllCredentials() async {
	        guard let output = try? await mobileIdWallet.fetchAllCredentials(.init()),
	        let credentialClaims = output.records.first?.claims else {
	            return
	        }
	        print(credentialClaims)
	    }
	}
    ```


## Delete Verifiable Credential 

Initiate  Feature intro 

=== "Android"

    ```kotlin
        ...
    ```

=== "iOS"

    ```swift
	import MobileIdWalletSDK
	
	class ManageCredentials {
	    let mobileIdWallet: MobileIdWalletProtocol
	    init(mobileIdWallet: MobileIdWalletProtocol) {
	        self.mobileIdWallet = mobileIdWallet
	    }
	}
	
	extension ManageCredentials {
	    func deleteCredential() async {
	        guard let output = try? await mobileIdWallet.fetchAllCredentials(.init()),
	        let credentialId = output.records.first?.id else {
	            return
	        }
	        _ = try? await mobileIdWallet.deleteCredential(.init(credentialId: credentialId))
	    }
	}
    ```

## Issue Verifiable Credential (Option 1)

Initiate  Feature intro 

=== "Android"

    ```kotlin
        ...
    ```

=== "iOS"

    ```swift
	import MobileIdWalletSDK
	import Foundation
	import WalletSDKCore
	
	class ManageCredentials {
	    let mobileIdWallet: MobileIdWalletProtocol
	    init(mobileIdWallet: MobileIdWalletProtocol) {
	        self.mobileIdWallet = mobileIdWallet
	    }
	}
	
	extension ManageCredentials {
	    func issueCredential() async {
	        let documentData = Model.PassportData(
	            id: UUID().uuidString ,
	            docIcaoCode: "",
	            docType: "",
	            isElectronic: true,
	            mrz: "",
	            name: "",
	            surname: "",
	            docNumber: "",
	            issueState: "",
	            expiryDate: "",
	            issueDate: "",
	            gender: "",
	            optionalData: "",
	            docImage: "",
	            holderImage: "",
	            biometricImage: "",
	            biometricFormat: "",
	            biometricSource: "",
	            docAuthStatus: ""
	        )
	        try? await mobileIdWallet.issueCredential(.init(documentData: documentData,
	                                                        type: .passport,
	                                                        requiresAuthenticationToCompleteFlow: true))
	    }
	}
    ```

## Issue Verifiable Credential (Option 2)

=== "Android"

    ```kotlin
        ...
    ```

=== "iOS"

    ```swift
	import MobileIdWalletSDK
	import Foundation
	import WalletSDKCore
	
	class ManageCredentials {
	    let mobileIdWallet: MobileIdWalletProtocol
	    init(mobileIdWallet: MobileIdWalletProtocol) {
	        self.mobileIdWallet = mobileIdWallet
	    }
	}
	
	extension ManageCredentials {
	    func readDocumentAndIssueCredential() async {
	        /// The `viewController` is required because the SDK needs a base view controller
	        /// to present the camera interface for document scanning. This should be the
	        /// screen from which the SDK is invoked.
	        let viewController = UIViewController()
	        try? await mobileIdWallet.readDocumentAndIssueCredential(.init(viewController: viewController, type: .passport))
	    }
	}
    ```