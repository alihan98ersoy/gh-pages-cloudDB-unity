---
title: "Code Development"
description: 30
---

## Code_Development
<img style="width: 250.00px ; padding: 5px" src="https://raw.githubusercontent.com/alihan98ersoy/gh-pages-cloudDB-unity/main/assets/unity.PNG">

```Please check out demo first```

```csharp
CloudDBService.cs
    //when press play button Subscribes Snapshot and starts to listen database realtime.
        public void Realtime()
            {
                CloudDBZoneQuery snapshotQuery = CloudDBZoneQuery.Where(new AndroidJavaClass(GameObjectTypeClass)).EqualTo("lobby","test");
                cloudDBManager.OnCloudDBZoneSnapshot = OnCloudDBZoneSnapshotSuccess;
                cloudDBManager.SubscribeSnapshot(snapshotQuery, CloudDBZoneQuery.CloudDBZoneQueryPolicy.CLOUDDBZONE_CLOUD_CACHE);
            }
//Then updates board with values using Gamamager.cs
       private void OnCloudDBZoneSnapshotSuccess(CloudDBZoneSnapshot<GameObjectType> snapshot)
    {
        CloudDBZoneObjectList<GameObjectType> gameObjectTypeCursor = snapshot.GetSnapshotObjects();
        List<GameObjectType> gameObjectTypeList = new List<GameObjectType>();
        try
        {
            while (gameObjectTypeCursor.HasNext())
            {
                GameObjectType gameObjectType = gameObjectTypeCursor.Next();
                gameObjectTypeList.Add(gameObjectType);
            }
            gameManager.UpdateWithData(gameObjectTypeList);
        }
        catch (Exception e){ }
        finally
        {
            snapshot.Release();
        }
    }    
```

```csharp
Gamemager.cs
    public void UpdateWithData(List<GameObjectType> list) 
	{
//if oCounter == xCounter it means player one can play. if not means player two's turn. 
		oCounter = 0;
		xCounter = 0;
//9 cell blocks starts with 1 array size is 10
		int[] integerArrayForWinnerCondition = new int[10];
		foreach (GameObjectType obj in list) 
		{
//first 9 is cell 10 and 11 is player info
			if (obj.Id < 10)
			{
                if (obj.Symbol == "-"||obj.Symbol == null) 
				{
					boardArray[obj.Id - 1].GetComponent<CellScript>().state = CellScript.CellStates.empty;
					integerArrayForWinnerCondition[obj.Id] = (int)CellScript.CellStates.empty;
				}
				else if (obj.Symbol.ToUpper() == "O") 
				{
					boardArray[obj.Id - 1].GetComponent<CellScript>().state = CellScript.CellStates.O;
					oCounter++;
					integerArrayForWinnerCondition[obj.Id] = (int)CellScript.CellStates.O;
				} 
				else if(obj.Symbol.ToUpper() == "X") 
				{
					boardArray[obj.Id - 1].GetComponent<CellScript>().state = CellScript.CellStates.X;
					xCounter++;
					integerArrayForWinnerCondition[obj.Id] = (int)CellScript.CellStates.X;
				}
			}
			else if (obj.Id == (int)ID.Player1) 
			{
				btn_Player1.GetComponent<UnityEngine.UI.Text>().text = obj.Name;
			}
			else if (obj.Id == (int)ID.Player2) 
			{
				btn_Player2.GetComponent<UnityEngine.UI.Text>().text = obj.Name;
			}
		}

//When reset button used this condition will triggered. Example opponent clicks reset your table and usernames will reset but your local device will think you did not //press. But reset action will effect both player.
		if (btn_Player1.GetComponent<UnityEngine.UI.Text>().text == "join" && btn_Player2.GetComponent<UnityEngine.UI.Text>().text == "join") 
		{
			currentPlayer = (int)CellScript.CellStates.empty;
			isPlayable = (int)PlayableStatus.Playable;
			txt_Plr1Wins.gameObject.SetActive(false);
			txt_Plr2Wins.gameObject.SetActive(false);
			txt_Draw.gameObject.SetActive(false);
		}
		CheckforWinner(integerArrayForWinnerCondition);
	}
//when click Play: starts listening Realtime Cloud DB
//when click Reset: updates all values as default
//when click join: if users login then updates the value for that player
//when click on board: if both users join the game then click board by turn updates that cell.
```

