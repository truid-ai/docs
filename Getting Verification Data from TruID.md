## Getting Data From Webhook
  1. Login to TruID dashboard using your username and password. 
  2. Specify the webhook url in the update profile section of the dashboard
  3. You will start receiving webhook notifications on the specified endpoint. The structure of data you will receive from the webhook is shared below

  ``` json
{
	"model": "api.session",
	"pk": 5256,
	"fields": {
		"chosen_agent": null,
		"agent": null,
		"report": {
			"latitude": 33.6460105,
			"longitude": 72.9963529,
			"ip_address": "127.0.0.1",
			"user_agent": "SM-A525F",
			"face_liveness": {
				"report": [{
						"key": "image_integrity",
						"value": "done",
						"children": [{
							"key": "face_present",
							"value": "done"
						}]
					},
					{
						"key": "face_integrity",
						"value": "done",
						"children": [{
							"key": "correct_action_performed",
							"value": "done"
						}]
					},
					{
						"key": "visual_authenticity",
						"value": "done",
						"children": [{
							"key": "face_match",
							"value": "done"
						}]
					}
				],
				"status": true,
				"retries": 1,
				"challenge": "right",
				"challenge_pose": "right"
			},
			"data_extraction": {
				"status": true
			},
			"document_capture": {
				"report": {
					"card": "SmartCNIC",
					"ocr_retries": 1,
					"extracted_data": {
						"Name": "Muhammad Abdullah Cheema",
						"Gender": "M",
						"Father Name": "Sohail Manzoor",
						"Date of Birth": "14.10.1997",
						"Date of Issue": "19.02.2016",
						"Date of Expiry": "19.02.2026",
						"Country of Stay": "Pakistan",
						"Identity Number": "37405-4950479-5"
					},
					"document_report": {
						"key": "data_validation",
						"value": "done",
						"children": [{
								"key": "issue_date_validation",
								"value": true
							},
							{
								"key": "expiry_date_validation",
								"value": true
							},
							{
								"key": " age_validation",
								"value": true
							},
							{
								"key": "gender_validation",
								"value": true
							},
							{
								"key": " id_number_validation",
								"value": true
							}
						]
					}
				},
				"status": true
			},
			"document_authenticity": {
				"report": [{
						"key": "visual_authenticity",
						"value": true,
						"children": [{
								"key": "template conformance",
								"value": true
							},
							{
								"key": "document_originality",
								"value": true
							}
						]
					},
					{
						"key": "data_validation",
						"value": "done",
						"children": [{
								"key": "issue_date_validation",
								"value": true
							},
							{
								"key": "expiry_date_validation",
								"value": true
							},
							{
								"key": " age_validation",
								"value": true
							},
							{
								"key": "gender_validation",
								"value": true
							},
							{
								"key": " id_number_validation",
								"value": true
							}
						]
					}
				],
				"status": true
			},
			"id_to_selfie_matching": {
				"report": {},
				"status": true
			}
		},
		"created_at": "2022-09-15T08:25:03.086Z",
		"updated_at": "2022-09-15T08:25:53.058Z",
		"status": "Verified",
		"client": 19,
		"meta": "meta"
	}
}
  ```
