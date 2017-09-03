using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class JoystickControl : MonoBehaviour {

    bool isCelelatePress = false;
    bool isDeCelelatePress = false;
    public float _X = 0f;
    public float _Y = 0f;

    private void Start()
    {
        StartCoroutine(TestCeleltePress());
        StartCoroutine(TestDeCeleltePress());
    }
    #region 摇杆
    // Use this for initialization
    public void LeftJoyStickMove(Vector2 direction)
    {

        _X = direction.x;
    }
    public void RightJoyStickMove(Vector2 direction)
    {
        _Y = direction.y;
    }

    public void LeftJoyStickMoveEnd( )
    {
        _X = 0f;
    }
    public void RightJoyStickMoveEnd()
    {
        _Y = 0f;
    }
    #endregion 
    public float GetVerticalInput()
    {
        return -_Y;
    }
    public float GetHorizontalInput()
    {
        return _X;
    }
    #region 前进后退按钮
    public void OnCeleltePressPress()
    {
        isCelelatePress = true;
    }

    public void OnCeleltePressPressUp()
    {
        isCelelatePress = false;
    }
    IEnumerator TestCeleltePress()
    {
        yield return new WaitForFixedUpdate();

        if (isCelelatePress)
        {
            _Y = Mathf.Clamp(_Y + 0.05f, 0f, 1f);
        }
        else if(!isDeCelelatePress)
        {
            _Y = 0f;
        }
        yield return TestCeleltePress();
    }



    public void OnDeCeleltePressPress()
    {
        isDeCelelatePress = true;
    }

    public void OnDeCeleltePressPressUp()
    {
        isDeCelelatePress = false;
    }

    IEnumerator TestDeCeleltePress()
    {
        yield return new WaitForFixedUpdate();

        if (isDeCelelatePress)
        {
            _Y = Mathf.Clamp(_Y - 0.05f, -1f, 0f);
        }
        else if(!isCelelatePress)
        {
            _Y = 0f;
        }
        yield return TestDeCeleltePress();
    }
    #endregion
}
