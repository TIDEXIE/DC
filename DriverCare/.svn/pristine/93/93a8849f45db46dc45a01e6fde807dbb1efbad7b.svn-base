using UnityEngine;
using System.Collections;

public class CameraFloor : MonoBehaviour
{
    public Transform target;
    public Transform target_FirstView;
    public float smothing = 5f;
    Vector3 offset;
    GameManager gameManager;
    // Use this for initialization
    void Start()
    {
        offset = transform.position - target.position;
        gameManager = GameObject.Find("GameControler").GetComponent<GameManager>();
    }

    // Update is called once per frame
    void FixedUpdate()
    {
        if (!gameManager.IsFirstPersonalView)
        {
            Vector3 targetCampos = target.position + offset;

            transform.position = Vector3.Lerp(transform.position, targetCampos, smothing * Time.deltaTime);//摄像机自身位置到目标位置
        }
        else
        {
            transform.position = target_FirstView.position;
            transform.rotation = target_FirstView.rotation;
        }
    }
}