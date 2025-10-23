# Subject Management

The Mobile ID Wallet SDK provides functionality to manage the relationships between passengers, flights, documents, and boarding passes. Developers can retrieve the current status of a subject using its unique identifier, allowing apps to track verification progress or workflow state. The SDK also supports creating and verifying subjects by associating a boarding pass with a document, linking passengers to their flights securely within the wallet. 

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
	            let documentId = "<YOUR_DOCUMENT_ID>"
	            let boardingPassId = "<YOUR_BOARDING_PASS_ID>"
	            do {
	                let output = try await mobileIdWallet.assocBoardingPassWithDocument(.init(
	                    viewController: viewController,
	                    documentId: documentId,
	                    boardingPassId: boardingPassId
	                ))
	                let subjectId = output.subjectId
	                // handle success here
	            } catch {
	                // handle error here
	            }
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
	            let subjectId = "<YOUR_SUBJECT_ID>"
	            do {
	                let output = try await mobileIdWallet.getSubjectStatus(.init(subjectId: subjectId))
	                let subjectStatus = output.subjectStatus
	                let subjectId = subjectStatus.id
	                let status = subjectStatus.status
	                // handle success here
	            } catch {
	                // handle error here
	            }
	
	        }
	    }
	}
    ```