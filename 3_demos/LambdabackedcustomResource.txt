from botocore.vendored import requests
import json
import uuid
def lambda_handler(event, context):
    try:
        if(event["RequestType"] == 'Create'):
            print('Create Success')
            sendResponse(event)
        elif(event["RequestType"] == 'Update'):
            print('Update Success')
            sendResponse(event)
        elif(event["RequestType"] == 'Delete'):
            print('Delete Success')
            sendResponse(event)
        else:
            raise Exception ('some error Occurred')
    except Exception as e:
        print e
        respObj = {
                   "Status" : "FAILED",
                   "PhysicalResourceId" : "none",
                   "StackId" : event["StackId"],
                   "RequestId" : event["RequestId"],
                   "LogicalResourceId" : event['LogicalResourceId'],
                   "Data" : {
                        "key" : "none"
                   }
                }
        respJson=json.dumps(respObj)
        requests.put(event["ResponseURL"], data = respJson)
def sendResponse(event):
    respObj = {
               "Status" : "SUCCESS",
               "PhysicalResourceId" : "none",
               "StackId" : event["StackId"],
               "RequestId" : event["RequestId"],
               "LogicalResourceId" : event['LogicalResourceId'],
               "Data" : {
                    "key" : "none"
               }
            }
    respJson=json.dumps(respObj)
    requests.put(event["ResponseURL"], data = respJson)