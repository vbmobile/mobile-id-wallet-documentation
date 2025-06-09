# Verifiable Credential 

This SDK provides a simple and flexible way to manage Verifiable Credentials, supporting full CRUD (Create, Read, Update, Delete) functionality. Whether you're issuing new credentials, retrieving stored ones, updating their contents, or securely deleting them, the SDK ensures a seamless integration experience.

Every function is available in both async/await and completion handler variants, allowing you to choose the approach that best suits your app's architecture. With a focus on performance and security, these operations help you manage credentials efficiently while keeping your implementation clean and maintainable.

## Get Passport Credentials (Verifiable Credentials)

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
	    func getPassportCredentials() async {
	        guard let output = try? await mobileIdWallet.getPassportCredentials(.init()),
	              let credentialClaims = output.records.first?.claims else {
	            return
	        }
	        print(credentialClaims)
	    }
	}
    ```

## Get original document used to create Passport Credential (Verifiable Credential) 

=== "Android"

	```kotlin
	val result = MobileIdWallet.getInstance().getDocumentReaderReport(
        activity = activity,
        params = GetDocumentReaderReport.Input(
            credentialId = credential.id
        )
    )
    if (result.isSuccess && result.getOrNull() != null) {
        val documentReaderReport = documentReaderReportOutput.getOrNull()?.documentReaderReport
        // handle success here
    } else {
        // handle error here
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
	
    func getOriginalDocumentForCreadential() {
        Task {
            /// Fetch all the credentials
            guard let output = try? await mobileIdWallet.getPassportCredentials(.init()),
                  let credential = output.records.first else {
                return
            }

            /// Using the credential id, fetch the origial `DocumentReaderReport` used to create the credential
            let documentReportOutput = try? await mobileIdWallet.getDocumentReport(.init(credentialId: credential.id))

            /// Original `DocumentReaderReport` used to create the credential
            guard let documentReaderReport = documentReportOutput?.originalDocument as? DocumentReaderReport else { return }
            let icaoCodeFromDocumentReaderReport = documentReaderReport.documentData.documentTypeData?.info?.icaoCode
            print(icaoCodeFromDocumentReaderReport)

            /// `Model.PassportData` is a model that contains in one place the most relevant fields of a `DocumentReaderReport` object
            guard let passportData = documentReaderReport.mapToPassportData as? Model.PassportData else { return }
            let icaoCodePassportData = passportData.docIcaoCode
            print(icaoCodePassportData)
        }
    }
    ```


## Delete Passport Credentials (Verifiable Credentials)

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
	    func deletePassportCredential() async {
	        guard let output = try? await mobileIdWallet.getPassportCredentials(.init()),
	              let credentialId = output.records.first?.id else {
	            return
	        }
	        _ = try? await mobileIdWallet.deletePassportCredential(.init(credentialId: credentialId))
	    }
	}
    ```

## Issue Passport Credential (Option 1) 

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
	    func issuePassportCredential() async {
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
	            expiryDate: "2025-01-01 00:00:00 +0000",
	            issueDate: "2035-01-01 00:00:00 +0000",
	            gender: "F",
	            optionalData: "20014361L",
	            docImage: "/9j/4AAQSkZJRgABAQAASABIAAD/4QCMRXhpZgAATU0AKgAAAAgABQESAAMAAAABA...", // Base64 Image
	            holderImage: "/9j/4AAQSkZJRgABAQAASABIAAD/4QCMRXhpZgAATU0AKgAAAAgABQESAAMAAA...", // Base64 Image
	            biometricImage: "/9j/4AAQSkZJRgABAQAASABIAAD/4QCMRXhpZgAATU0AKgAAAAgABQECCCC...", // Base64 Image
	            biometricFormat: "N/A",
	            biometricSource: "scan",
	            docAuthStatus: "false"
	        )
	        let output = try? await mobileIdWallet.issuePassportCredential(.init(
	            documentData: documentData,
	            type: .passport,
	            requiresAuthenticationToCompleteFlow: true
	        ))
	        guard let newCredential = output?.records.last else { return }
	        print(newCredential.claims)
	    }
	}
    ```

## Issue Passport Credential (Option 2) 

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
	    func readDocumentAndIssuePassportCredential() {
	        /// The `viewController` is required because the SDK needs a base view controller
	        /// to present the camera interface for document scanning. This should be the
	        /// screen from which the SDK is invoked.
	        let viewController = UIViewController()
	        Task {
	            let output = try? await mobileIdWallet.readDocumentAndIssuePassportCredential(.init(viewController: viewController, type: .passport))
	            guard let newCredential = output?.records.last else { return }
	            print(newCredential.claims)
	        }
	    }
	}
    ```
