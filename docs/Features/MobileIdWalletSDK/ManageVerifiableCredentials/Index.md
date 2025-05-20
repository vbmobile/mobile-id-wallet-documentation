# Verifiable Credential 

This SDK provides a simple and flexible way to manage Verifiable Credentials, supporting full CRUD (Create, Read, Update, Delete) functionality. Whether you're issuing new credentials, retrieving stored ones, updating their contents, or securely deleting them, the SDK ensures a seamless integration experience.

Every function is available in both async/await and completion handler variants, allowing you to choose the approach that best suits your app's architecture. With a focus on performance and security, these operations help you manage credentials efficiently while keeping your implementation clean and maintainable.

## Fetch Verifiable Credentials

=== "Android"

	```kotlin
	launch {
		val result = MobileIdWallet.getInstance().getPassportCredentials()
		
		if (result.isSuccess) {
			val credentials = result.getOrNull()
			// handle success here
		} else {
			// handle error here
		}
	}
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
    launch {
		val result = MobileIdWallet.getInstance().deletePassportCredential(
			input = DeletePassportCredential.Input(
				digitalIdID = digitalIdID
			)
		)
		if (result.isSuccess && result.getOrNull()?.success == true) {
			// handle success here
		} else {
			// handle error here
		}
	}
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
    launch {
		val documentData = Document(
			// TODO: fill document data
		)
		val result = MobileIdWallet.getInstance().issuePassportCredential(
			input = IssuePassportCredential.Input(
				documentData = documentData,
				type = DocumentType.Passport,
				requiresAuthenticationToCompleteFlow = true
			)
		)
		if (result.isSuccess && result.getOrNull()?.success == true) {
			// handle success here
		} else {
			// handle error here
		}
	}
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
	            id: UUID().uuidString,
	            docIcaoCode: "AUS",
	            docType: "passport",
	            isElectronic: true,
	            mrz: "P<AUSCITIZEN<<JANE<<<<<<<<<<<<<<<<<<<<<<<<<<D0996596<7AUS7906075F1812257<20014361L<<<<06",
	            name: "JANE",
	            surname: "CITIZEN",
	            docNumber: "D0996596",
	            issueState: "AUS",
	            expiryDate: "35-01-01",
	            issueDate: "25-01-01",
	            gender: "F",
	            optionalData: "20014361L",
	            docImage: "/9j/4AAQSkZJRgABAQAASABIAAD/4QCMRXhpZgAATU0AKgAAAAgABQESAAMAAAABA...", // Base64 Image
	            holderImage: "/9j/4AAQSkZJRgABAQAASABIAAD/4QCMRXhpZgAATU0AKgAAAAgABQESAAMAAA...", // Base64 Image
	            biometricImage: "/9j/4AAQSkZJRgABAQAASABIAAD/4QCMRXhpZgAATU0AKgAAAAgABQECCCC...", // Base64 Image
	            biometricFormat: "N/A",
	            biometricSource: "scan",
	            docAuthStatus: "false"
	        )
	        let output = try? await mobileIdWallet.issueCredential(.init(
	            documentData: documentData,
	            type: .passport,
	            requiresAuthenticationToCompleteFlow: true
	        ))
	        guard let newCredential = output?.records.last else { return }
	        print(newCredential.claims)
	    }
	}
    ```

## Issue Verifiable Credential (Option 2)

=== "Android"

    ```kotlin
    MobileIdWallet.getInstance().readDocumentAndIssueCredential(
		activity = requireActivity(),
		params = DocumentReaderParameters(true),
		callback = { result ->
			if (result.isSuccess && result.getOrNull()?.success == true) {
				val credentials = result.getOrNull()?.records
				// handle success here
			} else {
				// handle error here
			}
		}
	)
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
