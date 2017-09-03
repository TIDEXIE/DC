using System;
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class InputControler : MonoBehaviour {

    public GameObject Car;
    Transform m_transform;
    // Use this for initialization
    void Start () {
		if(Car!=null)
        {
            m_transform = Car.GetComponent<Transform>();
        }
        StartCoroutine("InitMoveSpeed");
	}
    //--缩放速度
    public float wheelSpeed = 50f;
    public float moveSpeed = 10f;
    public float MaxSpeed = 100f;
    // Update is called once per frame

    void Update () {
        //水平
        float h = Input.GetAxis("Horizontal");
        //垂直
        float v = Input.GetAxis("Vertical");

        m_transform.Translate(new Vector3(0, 0, -v * moveSpeed * Time.deltaTime));
        m_transform.Rotate(new Vector3(0, h * wheelSpeed * Time.deltaTime, 0));
        moveSpeed = Mathf.Clamp(moveSpeed + v, 0, MaxSpeed);
      
    }
    Vector3 oldPosition = new Vector3(0, 0, 0);
    Vector3 nowPosition = new Vector3(0, 0, 0);
    //private void FixedUpdate()
    //{
    //    nowPosition = transform.position;
    //    if(Mathf.Equals( nowPosition,oldPosition))
    //    {
    //        moveSpeed = 10;
    //    }
    //    oldPosition = nowPosition;
    //}

    IEnumerator InitMoveSpeed()
    {
        nowPosition = m_transform.position;
        //Debug.Log(string.Format("XIE CHENG:{0}", DateTime.Now.ToString()));
        yield return new WaitForSeconds(0.2f);
        Debug.Log(nowPosition);
        Debug.Log(oldPosition);
        if (nowPosition== oldPosition)
        {
 
            Debug.Log("false");
            moveSpeed = 10;
        }
        oldPosition = nowPosition;
        yield return InitMoveSpeed();
    }
}
