# Subject Management

A `Subject` consists of a set of data that represents a digital ID in the enrolment process. The Mobile ID SDK provides the ability to build and create such `Subject`. More info [__here.__](https://vbmobile.github.io/mobile-id-documentation/latest/Features/SubjectManagement/SubjectManagement_Index.html)

The Mobile ID Wallet SDK provides functionality to manage the relationships between passengers, flights, documents, and boarding passes. Developers can retrieve the current status of a subject using its unique identifier, allowing apps to track verification progress or workflow state. The SDK also supports creating and verifying subjects by associating a boarding pass with a document, linking passengers to their flights securely within the wallet. 


## Add Subject

You can create a new subject using the `assocBoardingPassWithDocument` method, that will do behind the scenes the `addSubject`. 

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
    ```

## Get Subject Status

After `assocBoardingPassWithDocument` a `Subject`, the id will be returned. This id can be used to get the `SubjectStatus` which will contain information about the current status of a given `Subject`. 

More info [__here.__](https://vbmobile.github.io/mobile-id-documentation/latest/Features/SubjectManagement/SubjectManagement_Index.html#subject-status)

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
    ```