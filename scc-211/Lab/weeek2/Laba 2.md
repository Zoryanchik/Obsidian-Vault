![[Pasted image 20251024003318.png]]![[Pasted image 20251024003437.png]]![[Pasted image 20251024003522.png]]![[Pasted image 20251024004040.png]]![[Pasted image 20251024004605.png]]![[Pasted image 20251024015717.png]]@startuml
left to right direction
actor authors
actor PC
actor Reviewer
rectangle "Conference Paper Review System" {
usecase asighn_unique_numbers_valid
usecase submit_papers
usecase validate_submission
usecase submit_review
usecase authors_offline_data
usecase Notify_Authors_of_Review_Results
usecase reject_submission
usecase notify_authors
usecase distribute_among_reviewers
authors--submit_papers
PC--notify_authors
PC--validate_submission
PC--Notify_Authors_of_Review_Results
Reviewer--submit_review
validate_submission.>asighn_unique_numbers_valid:<<extend>>
validate_submission.>reject_submission:<<extend>>
submit_papers.>authors_offline_data:<<include>>
submit_review.>Notify_Authors_of_Review_Results:<<include>>
reject_submission.>notify_authors:<<include>>
asighn_unique_numbers_valid.>distribute_among_reviewers:<<include>>
}


@enduml

- The system shall securely protect authors’ and reviewers’ data while ensuring only authorized access.
    
- The system shall handle high submission and review volumes efficiently without performance degradation.