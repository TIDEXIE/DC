using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.SceneManagement;

public class CommonMethod : MonoBehaviour {

    public void ExitGame()
    {
#if UNITY_EDITOR
		UnityEditor.EditorApplication.isPlaying = false;
        //SceneManager.LoadScene("");
#else
        Application.Quit();
#endif

    }
  
    public void OpenCarHouse()
    {
        SceneManager.LoadScene(ConstSetting.SCENCE_CARHOUSE);
    }
    public void CloseCarHouse()
    {

        //SceneManager.UnloadScene("CarHouse");
        //SceneManager.SetActiveScene(SceneManager.GetSceneByName("Cars"));
        SceneManager.LoadScene(ConstSetting.SCENCE_CARS);
    }
}
