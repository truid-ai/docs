
## Getting Data From server

-   Session data can be queried using this endpoing.
	``` curl
	curl --location --request GET '<truID backend URL>/sessions/<session-id>' --header 'Authorization: Api-Key <API-KEY goes here>'
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
						"Name": "string",
						"Gender": "string",
						"Father Name": "string",
						"Date of Birth": "string",
						"Date of Issue": "string",
						"Date of Expiry": "string",
						"Country of Stay": "string",
						"Identity Number": "string",
                                                "Permanent Address": "string",
                                                "Temporary Address": "string"
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
		"meta": "meta"
	}
	```
