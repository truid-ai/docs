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
			"latitude": 33.6460517,
			"longitude": 72.9963649,
			"ip_address": "127.0.0.1",
			"user_agent": "M2012K11AG",
			"undertaking": {
				"report": {},
				"status": true
			},
			"face_liveness": {
				"report": [
					{
						"key": "image_integrity",
						"value": "done",
						"children": [
							{
								"key": "face_present",
								"value": "done"
							}
						]
					},
					{
						"key": "face_integrity",
						"value": "done",
						"children": [
							{
								"key": "correct_action_performed",
								"value": "done"
							}
						]
					},
					{
						"key": "visual_authenticity",
						"value": "done",
						"children": [
							{
								"key": "face_match",
								"value": "done"
							}
						]
					}
				],
				"status": true,
				"retries": 1,
				"challenge": "left",
				"challenge_pose": "left"
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
							"chauhdry",
							"ahmed",
							"abbassi",
							"jibran",
							"nasir"
						],
						"Gender": "M",
						"cities": [
							"bahawalpur",
							"hyderabad",
							"karachi",
							"multan",
							"sukkur"
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
						"children": [
							{
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
				"report": {
					"hand": "right_4",
					"ring": 60,
					"index": 60,
					"thumb": null,
					"little": 60,
					"middle": 60,
					"retries": 0
				},
				"status": true
			},
			"verisys_verification": {
				"report": {},
				"status": true
			},
			"document_authenticity": {
				"report": [
					{
						"key": "visual_authenticity",
						"value": true,
						"children": [
							{
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
						"children": [
							{
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
				"report": {
					"status": true,
					"retries_left": 1,
					"mobile_number": "03123456789"
				},
				"status": true
			},
			"personal_information_verification": {
				"report": {
					"city": "bahawalpur",
					"name": "chauhdry"
				},
				"status": true
			}
		},
		"created_at": "2022-09-14T11:39:14.052311Z",
		"status": "Verified",
		"reference_frame": base64_string or null,
		"face_frame": base64_string or null,
		"agent_frame": null,
		"agent_pose_frame": null,
		"back_frame": base64_string or null,
		"pose_frame": null,
		"fingerprints": {
			"finger_1": {
				"image": link or null,
				"wsq": base64_string or null,
				"iso": base64_string or null,
			},
			"finger_2": {
				"image": link or null,
				"wsq": base64_string or null,
				"iso": base64_string or null,
			},
			"finger_3": {
				"image": link or null,
				"wsq": base64_string or null,
				"iso": base64_string or null,
			},
			"finger_4": {
				"image": link or null,
				"wsq": base64_string or null,
				"iso": base64_string or null,
			},
			"finger_5": {
				"image": link or null,
				"wsq": base64_string or null,
				"iso": base64_string or null,
			},
			"finger_6": {
				"image": link or null,
				"wsq": base64_string or null,
				"iso": base64_string or null,
			},
			"finger_7": {
				"image": link or null,
				"wsq": base64_string or null,
				"iso": base64_string or null,
			},
			"finger_8": {
				"image": link or null,
				"wsq": base64_string or null,
				"iso": base64_string or null,
			},
			"finger_9": {
				"image": link or null,
				"wsq": base64_string or null,
				"iso": base64_string or null,
			},
			"finger_10": {
				"image": link or null,
				"wsq": base64_string or null,
				"iso": base64_string or null,
			},
			"hand_type": "right_4"
		},
		"parsed_user_agent": "M2012K11AG",
		"authentication_video": null,
		"id": 5245,
		"time_consumed": "161.634052",
		"client_redirect_url": "https://release.truid.ai/test?client=ssdoNIiD.dikVmlPmc2t1HSd4SnZhFtAXuyBxDh7o",
		"meta": "meta"
	}
	```
