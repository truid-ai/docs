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
		"reference_frame": "https://truid-release-2.s3.amazonaws.com/1294dc84-d945-4967-94ff-cedeb7174a0f.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAQ76NEIDKMWYXEEH5%2F20220915%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20220915T120513Z&X-Amz-Expires=3600&X-Amz-SignedHeaders=host&X-Amz-Signature=024a20e9989f569a9b8b0fa4b6cf51558e6a99436496ef1e09f3c1d7be80111b",
		"face_frame": "https://truid-release-2.s3.amazonaws.com/b7f312e0-ab78-47a5-a0a9-67df1a4385c6.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAQ76NEIDKMWYXEEH5%2F20220915%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20220915T120513Z&X-Amz-Expires=3600&X-Amz-SignedHeaders=host&X-Amz-Signature=206fc40f86a677ea2194a0708a4ff4fd5079948dca586fb5ecb73e04b73c1112",
		"agent_frame": null,
		"agent_pose_frame": null,
		"back_frame": "https://truid-release-2.s3.amazonaws.com/48d0eb89-51a0-4492-93f3-ccfa8c172983.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAQ76NEIDKMWYXEEH5%2F20220915%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20220915T120513Z&X-Amz-Expires=3600&X-Amz-SignedHeaders=host&X-Amz-Signature=eca51cf22dcfd8d0404346a4e4e55b5d41cdc2ec71cc3520b8afa52597369346",
		"pose_frame": "https://truid-release-2.s3.amazonaws.com/94d6a269-747b-4a1e-a4cb-f98a8305c472.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAQ76NEIDKMWYXEEH5%2F20220915%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20220915T120513Z&X-Amz-Expires=3600&X-Amz-SignedHeaders=host&X-Amz-Signature=ac8b5a0e20b8b3caed6a7fdc0df58ac715857b8add130d429fd55044f6efe460",
		"fingerprints": {
			"finger_1": {
				"image": null,
				"wsq": null,
				"iso": null
			},
			"finger_2": {
				"image": "https://truid-release-2.s3.amazonaws.com/fingerprints/9f0de312-311f-4232-ba28-8aca1b963c6b.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAQ76NEIDKMWYXEEH5%2F20220915%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20220915T120513Z&X-Amz-Expires=3600&X-Amz-SignedHeaders=host&X-Amz-Signature=581d093c839c9abb0ce9cf8a68f5a27759af35784af6bdf4c993d1880afcae51",
				"wsq": "https://truid-release-2.s3.amazonaws.com/fingerprints/finger_2_95958720-EC1E-4B06-B524-04B902424086.wsq?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAQ76NEIDKMWYXEEH5%2F20220915%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20220915T120513Z&X-Amz-Expires=3600&X-Amz-SignedHeaders=host&X-Amz-Signature=b9ae7e932ce862e0e34c8e40b963b595eca70189fdefbaf6434cbdf259d56bb7",
				"iso": "Rk1SACAyMAAAAAFoAAABUAI6AMUAxQEAAgBQN0BxADYOJ0BXAD0SCoBEAGafJ4BVAIMbDEBXAIufDkB5ALeiNECGAM/APECAAPHASUBGANe5SUAxANEzPEAkANy2MUBuASHASYB6ATJARECPAX26EkCMAYs2EkBmAZM2LoBhAaQzFkBVAaZEBkBcAbcYA4BIAZ9RC0BWAY9AIkBMAcOABEBiAc4RB4BzAdQVEUCRAcEfN0CfAc0VPUDDAcUcRUDOAeMRPECtAfQOPYCwAZ4sQUDkAZIwTUDwAbImQkD9Ac4iMoEQAbcmPEERAdQbMkExAbIpEkD+AWE9SoDsAUfAREEGAS3ETIEnAUfGQoEuATHNQoE7AVrKD0ENAMXNSYDjALXRTYDWAMVLQkEPAJlURYEkAKXQPID2AG/lREEUAF9fOYDMAENwP0CrAJLwLEAYAVzAMUAnAaNVQYA2AbdfFkAyAcNiBQAA"
			},
			"finger_3": {
				"image": "https://truid-release-2.s3.amazonaws.com/fingerprints/eaba4d48-7d25-4ded-aee5-3619e2f294db.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAQ76NEIDKMWYXEEH5%2F20220915%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20220915T120513Z&X-Amz-Expires=3600&X-Amz-SignedHeaders=host&X-Amz-Signature=41412075bb8355ea9e4d43148d8cec0c9850be0838370982b3005d865cfc0028",
				"wsq": "https://truid-release-2.s3.amazonaws.com/fingerprints/finger_3_BC20DF00-06AF-447F-A890-7E16111736E7.wsq?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAQ76NEIDKMWYXEEH5%2F20220915%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20220915T120513Z&X-Amz-Expires=3600&X-Amz-SignedHeaders=host&X-Amz-Signature=5b19d08f92b7af9ef8115ba3095c4945615ae67f00c76860af5455771b93e2e0",
				"iso": "Rk1SACAyMAAAAAMwAAABiAJ2AMUAxQEAAwBQg4DLADz9MkC7AEt9OkCeAHwRRECIAHOXR4CZAKKYSkDbAIZzTEDhAKXrSkD9AIflSkEgAKNVOUEMAMNUPYExALnUEUEzALFREEEuAMDQL0FCAK3RHkE7AKFUHEE6AJdUEEFAAI/UD4FFAItRC0FAAHZYEUFTALFLC0FVAMFLIYFEAMzLCkE9ANNKEoFDANzKEoFEAONLEkFDAOvLEoFGAPFLEoFJAPnNEoFYAPNHIoFXAQdHKoFXASBEL4FWATRHN4E+ASjKN4FXAVNHLIFVAWhHEkFMAYDGD4FOAYVED0E1AXnARYFWAaq9EkFTAbU9EEFEAdIwKYEvAdmpCIEiAdwbAoEwAe4cE0EJAdqYA0EBAdQbBoD5AdAlDkD3Ad8SFoDuAcwzDIDrAcBOAEDyAbhEAED4Aaw9FIEAAbAwIkD1AaJEJ0DwAaJOLED/AZRAPIEPAZQ3QYEGAXdBQUDWAXDHEoDPAWNEEoDPAVnGEoDNAVJHEkDMARLHQUDEAQbAP0DFAPD8EkDIAOlzEoDsAPVOPUEIAOpLPUEZAPHHP0FUANZHMoCsARjGOkCVARnARUB1ARnAPYBwASg9EkB0ASzAEkBeAPY3KkBpAO+6JIBkANW2JkBEAO22P0BAANK1EkBFAMgzEkBfALYsREAeAKAsIoAzAGuiD4BCAF4bFoBAAFQYA4BLAE2YB4BTAFOYKUBdAEgYEoA4ATu2SUBNAWK5SYApAXmsSkA4AZ+2OUBOAaHAQUA3AbO5QoBvAcpOSkBVAeReRIBsAe1iOkBvAfpvEkB7AexfNICGAdpRRUCPAfhsEkCLAfxwEoCDAgj2EoBkAgXuEkBbAgpwEkBsAhR2EoCDAjSAPICkAiJ9LIClAgn2EkCmAf1wD0C2Af1zF0C2AehlOoDAAhOEEoDAAiMEEkDbAieEIUC6AlOOJkEEAiyVEUD7AgAOIYEfAiSXCUEiAjgYFoFBAg2eC0FFAgAfD4FTAgKsDYDiAd0OJEDZActbHIEhAbksPUCeAZdHEoCgAZDHEkA/AeVfNUAyAftvBwAA"
			},
			"finger_4": {
				"image": "https://truid-release-2.s3.amazonaws.com/fingerprints/a93e13c5-c33e-45d1-a53a-8c58b9288573.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAQ76NEIDKMWYXEEH5%2F20220915%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20220915T120513Z&X-Amz-Expires=3600&X-Amz-SignedHeaders=host&X-Amz-Signature=d332dfff9f692a6f6a1f8a62b9ad0ea9db6dc7ad3ad75287490ec3781cfb3387",
				"wsq": "https://truid-release-2.s3.amazonaws.com/fingerprints/finger_4_9159EEEF-AC3F-412D-8EC4-A2CE9EFAE5D8.wsq?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAQ76NEIDKMWYXEEH5%2F20220915%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20220915T120513Z&X-Amz-Expires=3600&X-Amz-SignedHeaders=host&X-Amz-Signature=830b3380d3589ff0360492d1e5daf4f5f3d6014c2a76abc9b0c0ee52ace1fcc7",
				"iso": "Rk1SACAyMAAAAAHIAAABSAJGAMUAxQEABABQR0B4ACOUIkCNACsLPEB/AEGXSkCWAEMOQUClACiDOUCoAFKERUC7AHJ9PEDSAHjwNYDaAIdsJ4DfAJbkNIDIALzfLEDhAMFRPIC9AMvHPICSANZAN4CMAMG9QkBjAMW8EkBkALo6EkBDAMQ6P0CBAJmwOUCHAH8iLoBKAHeyR0A0AHQwOUAuAGSsMUBlADQYMoBbACUbDUDqADJvGUD4ADvoGUERAFJiCUEUAMpKC4DfAPbGSUDdARdESYC9AQDHEoCvAPxHEkCfAPbEQkBTAQo6PEBPASG9NEBNATM6LEBJAUe8KkBfAUy9PUArARa5NYAnAWu8QYARAXG2DYAaAYHAMYAhAaZLKUAlAa5VHoAyAbBVJ0BHAbteN0BBAc1oRIBcAcpiQUB0AdJlOUCHAdBlKUCGAb9iJICcAd5pEYCnAcdbHEDCAchbGkDEAcBVIoDhAdJwHoDoAatbPED9AbtwMkD9AZ1RKkD2AZhLKUERAa1sMkEYAaBeNEEeAb96NUECAdp2EkESAYJLOUEqAX/QD0EHAWPHN0EGAVVEEkEQAVTGEoCsAWnHRQAA"
			},
			"finger_5": {
				"image": "https://truid-release-2.s3.amazonaws.com/fingerprints/c1138f7d-0e0e-4df9-986f-98d7dd27dbfd.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAQ76NEIDKMWYXEEH5%2F20220915%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20220915T120513Z&X-Amz-Expires=3600&X-Amz-SignedHeaders=host&X-Amz-Signature=0f84185a3ab04eea5e806b4c83cf851a8fbff8d09825c0e14d5d2214ac7b6059",
				"wsq": "https://truid-release-2.s3.amazonaws.com/fingerprints/finger_5_28C7F125-7C02-44EE-B049-F8E0EC1CB0E3.wsq?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAQ76NEIDKMWYXEEH5%2F20220915%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20220915T120513Z&X-Amz-Expires=3600&X-Amz-SignedHeaders=host&X-Amz-Signature=d51472ffa2f073a55ff18543b4bbf01a7c605fcea566b7e1633e26f5a259936e",
				"iso": "Rk1SACAyMAAAAAGAAAABDAG9AMUAxQEABQA8O4B/ABqKNEBtADYOLkBoAE6REIBaAFcfEIBWAIi1DoCAAKApBICMAKabAoCQALTUB0COAL9RDkCOANNUEoB9AMzVEoB8ANjVKoCPAOjNC4CXAO5LEICPAPbKEoBsAQLHEoBrAQxHEEBaAQTDHoBjARfHEkBhAShEKUBZAU5LMUBPAW1iMkBsAW1iLoB5AXdiD0B1AYLmD0BzAYtpEoBuAYlsEkB6AZXvEkCAAY1iEkBdAYlpEoBgAZbvEoBjAZ1sEkCKAalsD0CiAYJeL0CPAWNOGYC4AW9VD4CzAWHREkDKAWhUJECRATzHLkDhASfQBIDiASBUBEDTARfOJoDQAK1RCkDIAKzVC4C8AKRbEYCxAKPaC0CpAJ3hB4CkAKfUD4CsALLNGoCvAIfzNECbAIAJJ0CTAIkHD4DjAJFYB0DiAIjeC0DoAKTXCEDhAFZoJ0C6AD/1NUAvASC9E0AzAV1YLAAA"
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
