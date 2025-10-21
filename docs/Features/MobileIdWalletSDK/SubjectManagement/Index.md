# Subject Management

The Mobile ID Wallet SDK provides functionality to manage the relationships between passengers, flights, documents, and boarding passes. Developers can retrieve the current status of a subject using its unique identifier, allowing apps to track verification progress or workflow state. The SDK also supports creating and verifying subjects by associating a boarding pass with a document, linking passengers to their flights securely within the wallet. 

All operations support Swift’s async/await concurrency model and offer completion handler alternatives for legacy callback-based workflows. Inputs and outputs are strongly typed, ensuring safe and predictable access to subject and association data, while the API follows a consistent Swift-native design for seamless integration into your app.

## Add Subject

=== "Android"

    ```kotlin
    launch {
        val result = MobileIdWallet.getInstance().assocBoardingPassWithDocument(
            context = context,
            AssocBoardingPassWithDocument.Input(
                documentId = documentId,
                boardingPassId = boardingPassId,
            )
        )

        if (result.isSuccess) {
            val subjectId = result.getOrNull()?.subjectId
            // handle success here
        } else {
            // handle error here
        }
    }
    ```

=== "iOS"

    ```swift
	extension EnrolmentManagerSampleUsage {
	    /// Verifies and creates a subject, associates a passenger with a flight, and links a boarding pass with a document in the wallet.
	    func assocBoardingPassWithDocument() {
	        let viewController = UIViewController()
	        Task {
	            let documentId = "your_document_id"
	            let boardingPassId = "your_boarding_pass_id"
	            let result = try? await mobileIdWallet.assocBoardingPassWithDocument(.init(
	                viewController: viewController,
	                documentId: documentId,
	                boardingPassId: boardingPassId
	            ))
	            /// Returns the subject id
	            guard let subjectId = result?.subjectId else { return }
	            print(subjectId)
	        }
	    }
	}
    ```

## Get Subject Status

=== "Android"

    ```kotlin
    launch {
        val result = MobileIdWallet.getInstance().getSubjectStatus(
            GetSubjectStatus.Input(subjectId)
        )

        if (result.isSuccess) {
            val subjectId = result.getOrNull()?.subjectStatus
            // handle success here
        } else {
            // handle error here
        }
    }
    ```

=== "iOS"

    ```swift
	extension EnrolmentManagerSampleUsage {
	    /// Given a _subject id_, will return the `MobileIdSDKiOS.SubjectStatus`
	    func getSubjectStatus() {
	        Task {
	            let subjectId = "your_subject_id"
	            let output = try? await mobileIdWallet.getSubjectStatus(.init(subjectId: subjectId))
	            guard let subjectStatus = output?.subjectStatus else { return }
	            print(subjectStatus.id)
	            print(subjectStatus.status)
	        }
	    }
	}
    ```