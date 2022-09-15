## Getting Data From Webhook Notification
1. Login to TruID dashboard using your username and password. 
2. Specify the webhook url in the update profile section of the dashboard.<img width="1440" alt="image" src="https://user-images.githubusercontent.com/12184975/190359806-86d6a2f1-2545-4017-a722-76e118578c5e.png">

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

## Getting Data From server

-   Session data can be queried using this endpoing.
	``` curl
	curl --location --request GET 'https://release-api.truid.ai/sessions/<session-id>' --header 'Authorization: Api-Key <API-KEY goes here>'
	```
	This returns the session object, the structure of which is 
	``` json
	{
		"agent": null,
		"chosen_agent": null,
		"report": {
			"latitude": 31.5030094,
			"longitude": 74.3296054,
			"ip_address": "127.0.0.1",
			"user_agent": "M2012K11AG",
			"undertaking": {
				"report": {},
				"status": null
			},
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
				"challenge": "left",
				"challenge_pose": "TOO LEFT"
			},
			"data_extraction": {
				"status": true
			},
			"document_capture": {
				"report": {
					"card": "SmartCNIC",
					"ocr_retries": 1,
					"extracted_data": {
						"Name": "Mahad Majeed",
						"names": [
							"abbassi",
							"jabeen",
							"nasir",
							"ahmed",
							"sahkir"
						],
						"Gender": "M",
						"cities": [
							"larkana",
							"sialkot",
							"karachi",
							"gujranwala",
							"islamabad"
						],
						"Father Name": "Sh Abid Majeed",
						"Date of Birth": "27.01.1994",
						"Date of Issue": "18.11.2018",
						"Date of Expiry": "18.11.2028",
						"Country of Stay": "Pakistan",
						"Identity Number": "31202-3218074-9"
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
			"fingerprint_capture": {
				"report": {},
				"status": null
			},
			"verisys_verification": {
				"report": {},
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
			},
			"document_backside_capture": {
				"report": {},
				"status": true
			},
			"mobile_number_verification": {
				"report": {},
				"status": null
			},
			"personal_information_verification": {
				"report": {},
				"status": null
			}
		},
		"created_at": "2022-09-01T10:34:16.367442Z",
		"status": "Incomplete",
		"reference_frame": "https://truid-release-2.s3.amazonaws.com/b12a801a-bd54-45aa-a2f9-0f4b1127b7b7.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAQ76NEIDKMWYXEEH5%2F20220915%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20220915T113647Z&X-Amz-Expires=3600&X-Amz-SignedHeaders=host&X-Amz-Signature=28003d9a8e989e83597d3aa1257c71a323fa0285e23c7da45379c7d12151dc3d",
		"face_frame": "https://truid-release-2.s3.amazonaws.com/2c4ced67-4c74-4990-89e8-6397105df25b.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAQ76NEIDKMWYXEEH5%2F20220915%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20220915T113647Z&X-Amz-Expires=3600&X-Amz-SignedHeaders=host&X-Amz-Signature=12e8bb7d8a03d375d9534b2538277c7c83e3577c7f93c2c7c32ee742b97566bc",
		"agent_frame": null,
		"agent_pose_frame": null,
		"back_frame": "https://truid-release-2.s3.amazonaws.com/7c032d6b-c315-41f0-8c40-2fb5e8ed61ff.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAQ76NEIDKMWYXEEH5%2F20220915%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20220915T113647Z&X-Amz-Expires=3600&X-Amz-SignedHeaders=host&X-Amz-Signature=72a7ff7f071c6fd1fbad119b3a85f7547c1d260dbb097f8703cc7e0d4e4a8e7f",
		"pose_frame": "https://truid-release-2.s3.amazonaws.com/7e118a5c-545a-4c8a-a02d-0a4a9b9cb752.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAQ76NEIDKMWYXEEH5%2F20220915%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20220915T113647Z&X-Amz-Expires=3600&X-Amz-SignedHeaders=host&X-Amz-Signature=4c6df202569ba859c76e1fbb86d73927109feae07304503e135e8b9f9fde7392",
		"fingerprints": {
			"finger_1": {
				"image": null,
				"wsq": null,
				"iso": null
			},
			"finger_2": {
				"image": null,
				"wsq": null,
				"iso": null
			},
			"finger_3": {
				"image": null,
				"wsq": null,
				"iso": null
			},
			"finger_4": {
				"image": null,
				"wsq": null,
				"iso": null
			},
			"finger_5": {
				"image": null,
				"wsq": null,
				"iso": null
			},
			"finger_6": {
				"image": null,
				"wsq": null,
				"iso": null
			},
			"finger_7": {
				"image": null,
				"wsq": null,
				"iso": null
			},
			"finger_8": {
				"image": null,
				"wsq": null,
				"iso": null
			},
			"finger_9": {
				"image": null,
				"wsq": null,
				"iso": null
			},
			"finger_10": {
				"image": null,
				"wsq": null,
				"iso": null
			},
			"hand_type": null
		},
		"parsed_user_agent": "M2012K11AG",
		"authentication_video": null,
		"id": 5167,
		"time_consumed": "19.473962",
		"client_redirect_url": "https://release.truid.ai/test?client=ssdoNIiD.dikVmlPmc2t1HSd4SnZhFtAXuyBxDh7o",
		"meta": "meta"
	}
	```
