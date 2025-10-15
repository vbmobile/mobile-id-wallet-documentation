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
	
	class ManageEnrolment {
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
	extension ManageEnrolment {
	    func assocBoardingPassWithDocument() {
	        let viewController = UIViewController()
	        Task {
	            guard let output = try? await mobileIdWallet.getAllBoardingPass(),
	                  let boardingPassId = output.records.first?.id else { return }
	
	            guard let output = try? await mobileIdWallet.getAllDocuments(),
	                  let documentId = output.records.first?.id else { return }
	
	            _ = try? await mobileIdWallet.assocBoardingPassWithDocument(.init(
	                viewController: viewController,
	                documentId: documentId,
	                boardingPassId: boardingPassId
	            ))
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
    func getSubjectStatus() {
        let viewController = UIViewController()
        Task {
            guard let output = try? await mobileIdWallet.getAllBoardingPass(),
                  let boardingPassId = output.records.first?.id else { return }

            guard let output = try? await mobileIdWallet.getAllDocuments(),
                  let documentId = output.records.first?.id else { return }

            let assocBoardingPassWithDocumentOutput = try? await mobileIdWallet.assocBoardingPassWithDocument(.init(
                viewController: viewController,
                documentId: documentId,
                boardingPassId: boardingPassId
            ))
            if let subjectId = assocBoardingPassWithDocumentOutput?.subjectId {
                let getSubjectStatusOutput = try? await mobileIdWallet.getSubjectStatus(.init(subjectId: subjectId))
                if let subjectStatus = getSubjectStatusOutput?.subjectStatus {
                    print(subjectStatus.id)
                    print(subjectStatus.status)
                }
            }
        }
    }
    ```