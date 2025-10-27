# Misc Operations

The Mobile ID Wallet SDK provides additional utility functions to simplify wallet management. This includes operations such as batch deleting multiple documents or boarding passes at once, allowing developers to efficiently manage wallet contents. These miscellaneous functions complement the main workflows for document and boarding pass handling, providing flexibility and control over stored data.
	
## Batch Delete

=== "Android"

    ```kotlin
	launch {
        val result = MobileIdWallet.getInstance().batchDelete()

        if (result.isSuccess) {
            // handle success here
        } else {
            // handle error here
        }
    }
    ```

=== "iOS"

    ```swift
	mobileIdWallet.batchDelete()
	```

## Exceptions handling

=== "Android"

    ```kotlin
	
    ```

=== "iOS"

    ```swift
    /// Demonstrates a `WalletSDKError.dataBase(.duplicatedRecord)` scenario.
    ///
    /// In this example, a boarding pass is associated with a document twice,
    /// triggering a database-level duplication error.
    func duplicatedRecord() {
        let topViewController = UIViewController()

        Task {
            do {
                let readDocumentOutput = try await mobileIdWallet.readDocument(.init(
                    viewController: topViewController,
                    readDocumentParameters: .init(readRFID: true)
                ))

                let readBoardingPassOutput = try await mobileIdWallet.scanBoardingPass(.init(
                    viewController: topViewController,
                    parameters: .init(validateBoardingPass: true)
                ))

                // First association succeeds.
                _ = try await mobileIdWallet.assocBoardingPassWithDocument(.init(
                    viewController: UIViewController(),
                    documentId: readDocumentOutput.document.id,
                    boardingPassId: readBoardingPassOutput.boardingPass.id
                ))

                // Attempting the same association again will throw:
                // `WalletSDKError.dataBase(.duplicatedRecord)`
                _ = try await mobileIdWallet.assocBoardingPassWithDocument(.init(
                    viewController: UIViewController(),
                    documentId: readDocumentOutput.document.id,
                    boardingPassId: readBoardingPassOutput.boardingPass.id
                ))

            } catch {
                if let error = error as? WalletSDKError {
                    // Uses your computed property for a localized, user-safe message
                    print(error.publicMessage)
                }
            }
        }
    }
    ```