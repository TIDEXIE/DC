using System;
using System.Collections;
using UnityEngine;
using UnityEngine.SceneManagement;
using UnityEngine.UI;

public class GameManager : MonoBehaviour {

    // Use this for initialization
    public Text TimeText;
    public Text VelocityText;
    /// <summary>
    /// 是否第一人称视角
    /// </summary>
    public bool IsFirstPersonalView=true;
    DateTime startTime;
    Rigidbody CarRigidbody;
    public GameObject particleSmoke;
    public GameObject stopLight;
    /// <summary>
    ///摇杆输入
    /// </summary>
    JoystickControl JoystickControler;
    void Start () {
        
        TimeText = GameObject.Find("Canvas/TimeText").GetComponent<Text>();
        VelocityText = GameObject.Find("Canvas/VelocityText").GetComponent<Text>();
        CarRigidbody = GameObject.Find("FireGTO").GetComponent<Rigidbody>();
        stopLight= GameObject.Find("FireGTO/GTO_Body/StopLight");

        JoystickControler = GameObject.Find("GameControler").GetComponent<JoystickControl>();

        startTime = DateTime.Now;
        //particleSmoke = GameObject.Find("FireGTO/Particles");
        StartCoroutine("SmokeParticles");
        StartCoroutine(StopLight());

    }


    IEnumerator SmokeParticles()
    {
        yield return new WaitForSeconds(1.1f);
        if (CarRigidbody.velocity.sqrMagnitude>50)
        {
            particleSmoke.SetActive(true);
        }
        else
        {
            particleSmoke.SetActive(false);
        }
       
        yield return SmokeParticles();
    }

    IEnumerator StopLight()
    {
        yield return new WaitForSeconds(1.1f);
        //垂直
#if UNITY_ANDROID || UNITY_IPHONE
        float v = -JoystickControler.GetVerticalInput();
#endif
#if UNITY_STANDALONE_WIN
          float v = -Input.GetAxis("Vertical");
#endif
        if (v < 0)
        {
            stopLight.SetActive(true);
        }
        else
        {
            stopLight.SetActive(false);
        }
        yield return StopLight();
    }
    // Update is called once per frame
    void Update () {
        TimeText.text= GetTimeText();
        VelocityText.text =string.Format("当前车速：{0}km/h",(int) CarRigidbody.velocity.sqrMagnitude);
    }

  public  void StartGame()
    {
        PlayerPrefs.SetString(ConstSetting.BACKSCENE, "Menu");
        SceneManager.LoadScene("GameScene_0");
    }

    public void BackScene()
    {

        string backScene = PlayerPrefs.GetString( ConstSetting.BACKSCENE);
        //string backScene = "Menu";
        SceneManager.LoadScene(backScene);
    }
    public void ExitGame()
    {
        #if UNITY_EDITOR
		UnityEditor.EditorApplication.isPlaying = false;
        //SceneManager.LoadScene("");
        #else
		Application.Quit();
        #endif
        
    }
    public void ResetGame()
    {
        SceneManager.LoadScene(0);
        startTime = DateTime.Now;
    }
    public void ChangeView()
    {
        IsFirstPersonalView = !IsFirstPersonalView;
    }
    public void OpenCarHouse()

    {;
        SceneManager.LoadSceneAsync(ConstSetting.SCENCE_CARHOUSE);
        SceneManager.SetActiveScene(SceneManager.GetSceneByName(ConstSetting.SCENCE_CARHOUSE));
    }
    public void CloseCarHouse()
    {
      
        SceneManager.UnloadSceneAsync(ConstSetting.SCENCE_CARHOUSE);
    }
    string GetTimeText()
    {
        var deltaTime = DateTime.Now - startTime;
        string timeFormat = "已用时间：{2}h {1}min {0}s";
        if (deltaTime.Hours > 0)
        {
            timeFormat = "已用时间：{2}h {1}min {0}s";
        }
        else if (deltaTime.Minutes > 0)
        {
            timeFormat = "已用时间： {1}min {0}s";
        }
        else
        {
            timeFormat = "已用时间：{0}s";
        }
        return string.Format(timeFormat, deltaTime.Seconds, deltaTime.Minutes, deltaTime.Hours);
    }
}
