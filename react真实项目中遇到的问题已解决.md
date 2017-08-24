### react  步步维艰 
##### 图片引入 或 背景图片的路径
1.引入图片 

	//通过 import 来引入了。 接着jsx中的js表达式要写在{}中。 
	
	import protrait from '../images/portrait.png'
	
	<img src={ protrait } >
	
2.作为背景图使用 在css文件中需要用的url()
	
	npm install url-loader --save-dev
	
	//通过安装url-loader我们就可以在react&webpack项目中成功处理相对路径的问题。 
	
	//实际上也就是直接使用即可，因为url-loader解决的问题就是将路径成为可以处理的。	
	div.phone {
            background: url('../images/phone.png') no-repeat ;
        }

##### 渲染数组或者对象
这个是我要循环的数组

	allDetails:[
      {
        year:'2017',
        yearDetails:[
          {
            date:'12.11',
            consumeName:'医保消费',
            money:'-200.00'
          },
          {
            date:'11.11',
            consumeName:'医保消费',
            money:'-200.00'
          },
          {
            date:'10.11',
            consumeName:'医保消费',
            money:'-200.00'
          },
          {
            date:'09.11',
            consumeName:'医保消费',
            money:'-200.00'
          },
          {
            date:'08.11',
            consumeName:'医保消费',
            money:'-200.00'
          },
          {
            date:'07.11',
            consumeName:'医保消费',
            money:'-200.00'
          }
        ]
      },
      {
        year:'2016',
        yearDetails:[
          {
            date:'11.11',
            consumeName:'医保消费',
            money:'-200.00'
          },
          {
            date:'10.11',
            consumeName:'医保消费',
            money:'-200.00'
          },
          {
            date:'09.11',
            consumeName:'医保消费',
            money:'-200.00'
          },
          {
            date:'07.11',
            consumeName:'医保消费',
            money:'-200.00'
          },
          {
            date:'06.11',
            consumeName:'医保消费',
            money:'-200.00'
          },
          {
            date:'05.11',
            consumeName:'医保消费',
            money:'-200.00'
          }
        ]
      }
    ]
    
    
这个是我在render中写的

	
	{
            this.state.allDetails.map(
              function( years,i ){
                return(
                  <div className="one_year" key={i} >
                    <div className="detail_year" > { years.year } </div>
                    {
                      years.yearDetails.map(
                        function( yearDetails,i ){
                          return(
                            <div className="detail_row" key={i}>
                              <div className="words">
                                <div>{ yearDetails.date }</div>
                                <div className="words_in">{ yearDetails.consumeName }</div>
                              </div>
                              <div className="detail_num">{ yearDetails.money }</div>
                            </div>
                          )
                        }
                      )
                    }
                  </div>
                )

              }
            )
          }
          
      
 注意：`key  每个循环的item 必须要有唯一的 key `（ key 写在了<div></div>中 key用到的是js的 参数 所以 写法 `<div kye={ index } ></div>` ）	
 
 
 
 
##### 模拟单选的tab

state中的声明
	
	tabs:[
        {tabName:"全部",id:1},
        {tabName:"近三月",id:2},
        {tabName:"近半年",id:3},
        {tabName:"近一年",id:4},
      ],
      currentIndex:0,//tabs初始值的设置
      
 
render

	<div className="time_options">
            {
              this.state.tabs.map(function(tab,i){
                var tabStyle=tab.id==this.state.currentIndex ? 'options_active' : 'options';
                return(
                  <div className={ tabStyle } key={ i } onClick={ this.tabChoiced.bind(_this,tab.id) }>{ tab.tabName }</div>
                )
              }.bind(_this))
            }
          </div>
          
          
onClick：tabChoiced ES6写法

	tabChoiced=(id)=>{ //切换tab标签
      this.setState({
          currentIndex:id
      });
    }

	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
