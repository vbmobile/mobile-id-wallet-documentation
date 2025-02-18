# Intro

## Async/Await vs Completion Handlers

This SDK is built with flexibility in mind, offering both modern async/await support and traditional completion handlers for all functions. Whether you prefer the clarity of Swift Concurrency or need backward compatibility, you can choose the approach that best fits your project.

Why Both?

* Async/Await provides a cleaner, more readable way to handle asynchronous tasks, reducing nested closures and improving maintainability.
* Completion Handlers ensure compatibility with older iOS versions and existing callback-based architectures.

## Async/Await vs Completion Handlers sample

=== "Android"

    ```kotlin
        ...
    ```

=== "iOS"

    ```swift
	import MobileIdWalletSDK

	class ClosureVsAssync {
    	let mobileIdWallet: MobileIdWalletProtocol
    	init(mobileIdWallet: MobileIdWalletProtocol) {
        	self.mobileIdWallet = mobileIdWallet
    	}

	    func fetchAllCredentialsAssync() {
	        Task {
	            do {
	                let output = try await mobileIdWallet.fetchAllCredentials(.init())
	                print(output.records.first?.claims)
	            } catch {
	                print(error)
	            }
	        }
	    }
	    
	    func fetchAllCredentialsCompletionHandler() {
	        mobileIdWallet.fetchAllCredentials(.init()) { result in
	            switch result {
	            case .success(let output):
	                print(output.records.first?.claims)
	            case .failure(let error):
	                print(error)
	            }
	        }
	    }
	}

    ```

