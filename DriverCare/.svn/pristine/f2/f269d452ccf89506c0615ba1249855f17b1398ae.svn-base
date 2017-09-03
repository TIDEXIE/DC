using UnityEngine;
using System.Collections;

public class CarControl : MonoBehaviour
{

    //操纵前轮，用于转向
    public WheelCollider FrontLeftWheel;
    public WheelCollider FrontRightWheel;
    Quaternion FrontWheelRotation;

    public WheelCollider BackLeftWheel;
    public WheelCollider BackRightWheel;
    Quaternion BackWheelRotation;
    //齿轮转速数组
    public float[] GearRatio;
    //当前档位
    public int CurrentGear = 0;

    public float wheelSpeed = 20f;
    public float EngineTorgue = 600.0f;
    public float MaxEngineRPM = 3000.0f;
    public float MinEngineRPM = 1000.0f;
    private float EngineRPM = 0.0f;
 
    /// <summary>
    /// 刚体
    /// </summary>
    Rigidbody m_Rigidbody;
    /// <summary>
    /// 换挡声音
    /// </summary>
    AudioSource m_Audio;
    /// <summary>
    ///摇杆输入
    /// </summary>
    JoystickControl JoystickControler;
    void Start()
    {
        m_Rigidbody = GetComponent<Rigidbody>();
        m_Audio = GetComponent<AudioSource>();
        //设置车的重心，使车更稳定        
        Vector3 centerOfMass = m_Rigidbody.centerOfMass;
        centerOfMass.y = -1.5f;
        m_Rigidbody.centerOfMass = centerOfMass;

        FrontWheelRotation = FrontLeftWheel.transform.rotation;
        BackWheelRotation = BackLeftWheel.transform.rotation;

        JoystickControler= GameObject.Find("GameControler").GetComponent<JoystickControl>();
    }

    // Update is called once per frame
    void Update()
    {

#if UNITY_ANDROID || UNITY_IPHONE
        float v = JoystickControler.GetVerticalInput();
        float h = JoystickControler.GetHorizontalInput();
#endif
#if UNITY_STANDALONE_WIN
          float v = -Input.GetAxis("Vertical");
        float h = Input.GetAxis("Horizontal");
#endif

        //限制车的最大速度，调整阻力可能不是最好的做法。但它很简单，而且不会干扰物理系统的运行。
        m_Rigidbody.drag = m_Rigidbody.velocity.magnitude / 250;
        //通过两个轮子的平均rpm，计算引擎rpm，然后切换档位
        EngineRPM = (FrontLeftWheel.rpm + FrontRightWheel.rpm) / 2 * GearRatio[CurrentGear];
        ShiftGears();

        //设置换档的声音
        m_Audio.pitch = Mathf.Abs(EngineRPM / MaxEngineRPM) + 1.0f;
        if (m_Audio.pitch > 2.0)
        {
            m_Audio.pitch = 2.0f;
            if (!m_Audio.isPlaying)
                m_Audio.Play();
        }

        //最后设置轮子转动力矩。引擎力矩除以当前档位，乘以用户输入值。
        //轮子力矩提供一个汽车前进的力。轮子的转动又会提高档位。
        

        BackLeftWheel.motorTorque = EngineTorgue / GearRatio[CurrentGear] * v;
        BackRightWheel.motorTorque = EngineTorgue / GearRatio[CurrentGear] * v;

       int  a = (int)(GearRatio[CurrentGear] * FrontLeftWheel.rpm * 4);
        BackLeftWheel.transform.localEulerAngles += new Vector3(a, 0, 0);
        BackRightWheel.transform.localEulerAngles += new Vector3(a, 0, 0);

        //转动角度是任意数乘以用户输入值
      
        FrontLeftWheel.steerAngle = wheelSpeed * h;
        FrontRightWheel.steerAngle = wheelSpeed * h;

        int b =(int) (GearRatio[CurrentGear] * FrontLeftWheel.rpm* 4);
        FrontLeftWheel.transform.localEulerAngles += new Vector3(b, 0,0); 
        FrontRightWheel.transform.localEulerAngles += new Vector3(b, 0, 0); 
    }

    //private void OnGUI()
    //{
    //    if (GUI.Button(new Rect(30, 10, 150, 100),FrontLeftWheel.rpm.ToString()))
    //        print("You clicked the button!");

    //}
    /// <summary>
    /// 换档位
    /// </summary>
    void ShiftGears()
    {
        int AppropriateGear = CurrentGear;
        if (EngineRPM >= MaxEngineRPM)
        {
            AppropriateGear = CurrentGear;
            for (int i = 0; i < GearRatio.Length; i++)
            {
                if (FrontLeftWheel.rpm * GearRatio[i] < MaxEngineRPM)
                {
                    AppropriateGear = i;
                    break;
                }
            }
            CurrentGear = AppropriateGear;
        }

        if (EngineRPM <= MaxEngineRPM)
        {
            AppropriateGear = CurrentGear;
            for (int j = GearRatio.Length - 1; j >= 0; j--)
            {
                if (FrontLeftWheel.rpm * GearRatio[j] > MinEngineRPM)
                {
                    AppropriateGear = j;
                    break;
                }
            }
            CurrentGear = AppropriateGear;
        }

        //Debug.Log(string.Format("当前挡位：{0}", FrontLeftWheel.rpm));
    }
}