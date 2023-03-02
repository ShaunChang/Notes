# 1 card练习中的shadow
 box-shadow: rgb(50 50 93 / 25%) 0px 30px 60px -12px,

    rgb(0 0 0 / 30%) 0px 18px 36px -18px;


# 2 hover缩放：
/* Grow-Shadow */
.hvr-grow-shadow {
display: inline-block;
vertical-align: middle;
-webkit-transform: perspective(1px) translateZ(0);
transform: perspective(1px) translateZ(0);
box-shadow: 0 0 1px rgba(0, 0, 0, 0);
-webkit-transition-duration: 0.3s;
transition-duration: 0.3s;
-webkit-transition-property: box-shadow, transform;
transition-property: box-shadow, transform;
}
.hvr-grow-shadow:hover, .hvr-grow-shadow:focus, .hvr-grow-shadow:active {
box-shadow: 0 10px 10px -10px rgba(0, 0, 0, 0.5);
-webkit-transform: scale(1.1);
transform: scale(1.1);
}


# 3 hover边框发光
box-shadow: 0 0 10px rgb(0,153,184) inset,0 0 30px rgb(0,153,184);

# 4 hover button发光
background-color: #b9e769;
                                -webkit-box-shadow: 10px 10px 99px 6px rgba(185, 231, 105, 1);
                                -moz-box-shadow: 10px 10px 99px 6px rgba(185, 231, 105, 1);
                                box-shadow: 10px 10px 99px 6px rgba(185, 231, 105, 1);


# 5 光滑过特效 按钮
 <div class="nav__login--index">
            <form action="index.html" >
                <button><span>登录</span></button>
            </form>    
        </div>
                &--index {
                margin-right: 2*$fontsize;
                @include flexCenter();
               
                & button{
                    border: 2px solid white;
                    background: transparent;
                    text-transform: uppercase;
                    color: white;
                    padding: 15px 50px;
                    outline: none;
                    overflow: hidden;
                    position: relative;
                }
                & span {
                    z-index: 20;  
                  }
                & :after {
                    content: '';
                      display: block;
                      position: absolute;
                      top: -36px;
                      left: -100px;
                      background: white;
                      width: 50px;
                      height: 125px;
                      opacity: 20%;
                      transform: rotate(-45deg);
                  }
                  
                  & :hover :after {
                    left: 120%;
                    transition: all 600ms cubic-bezier(0.3, 1, 0.2, 1);
                     -webkit-transition: all 600ms cubic-bezier(0.3, 1, 0.2, 1);
                  }
            }

# 6 圆圈
border-radius:50%

# 7 浅灰色背景色和尿囊型border
  border-radius: 999em;
    background-color: rgba(246,246,246,0.8);;


# 8 调整container里面的icon size大小：
    .container{
        font-size: xxpx;
    }