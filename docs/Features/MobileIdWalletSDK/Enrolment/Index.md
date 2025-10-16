# Enrolment

TO DO

## Setup

=== "Android"

    ```kotlin
	 TO DO
    ```

=== "iOS"

    ```swift
	import Foundation
	import WalletSDKCore
	import MobileIdWalletSDK
	import MobileIdSDKiOS // MobileID (VB Enrollment SDK)
	
	class EnrolmentManagerSampleUsage {
	    let mobileIdWallet: MobileIdWalletProtocol
	    init(mobileIdWallet: MobileIdWalletProtocol) {
	        self.mobileIdWallet = mobileIdWallet
	    }
	}
    ```

## Add Subject

=== "Android"

    ```kotlin
	 TO DO
    ```

=== "iOS"

    ```swift
	extension EnrolmentManagerSampleUsage {
	    
	    /// Verify and create a Subject (connects a passanger with a fligth)
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
	 TO DO
    ```

=== "iOS"

    ```swift
	extension EnrolmentManagerSampleUsage {
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