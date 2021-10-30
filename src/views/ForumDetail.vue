<template>
  <el-container>
    <el-header>
      <el-breadcrumb separator="/">
        <el-breadcrumb-item :to="{ path: '/' }">首页</el-breadcrumb-item>
        <el-breadcrumb-item><a href="/">{{forum.name}}</a></el-breadcrumb-item>
      </el-breadcrumb>
    </el-header>
    <el-main>
      <el-card class="box-card">
        <div slot="header"
             class="clearfix" style="box-shadow: 0 2px 4px rgba(0, 0, 0, .12), 0 0 6px rgba(0, 0, 0, .04)">
          <div class="wrapper">
            <img class="img" style="width: 200px; height: 200px;"
                 src="../assets/img/os1.jpg">
            <div class="text">
              【推荐语】<br>
              用诙谐幽默语言讲述的深入理解操作系统原理的精品 轻松自制操作系统 操作系统并不深奥 本书给予全新解读<br/>
              【作者】<br/>
              郑钢，毕业于北京大学，前百度运维高 级工程师，对操作系统有深入的研究。好运动，喜钻研，热衷于尝试前沿技术，乐于分享学习成果。<br/>
              【内容】<br/>
              本书共分16章，讲解了开发一个操作系统需要的技术和知识，主要内容有：操作系统基础、部署工作环境、编写MBR主引导记录、完善MBR错误、保护模式入门、保护模式进阶和向内核迈进、中断、内存管理系统、线程、输入输出系统、用户进程、完善内核、编写硬盘驱动程序、文件系统、系统交互等核心技术。 本书适合程序员、系统底层开发人员、操作系统爱好者阅读，也可作为大专院校相关专业师生用书和培训学校的教材。
            </div>
          </div>
        </div>
        <el-tabs v-model="activeName" @tab-click="handleClick">
          <el-tab-pane label="笔记" name="first">
            <NoteList :noteList="notes"/>
          </el-tab-pane>
          <el-tab-pane label="问题" name="second">
            <QuestionList :questionList="questions"/>
          </el-tab-pane>
        </el-tabs>
      </el-card>
    </el-main>
  </el-container>

</template>

<script>
import NoteList from '@/components/NoteList.vue'
import QuestionList from '@/components/QuestionList.vue'

export default {
  name: 'ForumDatail',
  components: {
    NoteList,
    QuestionList
  },
  data() {
    return {
      activeName: 'first',
      forum: {
        id: 1,
        name: '操作系统真相还原',
      },
      notes: [
        {
          id: 1,
          title: "中断和中断处理程序",
          abstract: "本次笔记记录了CPU中断是什么？中断类型有哪些？如何设置中断处理程序？本次笔记记录了CPU中断是什么？中断类型有哪些？如何设置中断处理程序？本次笔记记录了CPU中断是什么？中断类型有哪些？如何设置中断处理程序？本次笔记记录了CPU中断是什么？中断类型有哪些？如何设置中断处理程序？",
          author: {
            name: "带ta去蒙古国",
            avatar: "https://pic1.zhimg.com/v2-bb2aa7b20551744a027d8ea9dbcc03c6_xs.jpg"
          },
          viewCount: 10,
          commentCount: 100,
          statCount: 1000,
          tagList: [
            {
              tagId: 1,
              tagName: "javaScript"
            },
            {
              tagId: 2,
              tagName: "javaScript"
            },
            {
              tagId: 3,
              tagName: "javaScript"
            },
            {
              tagId: 4,
              tagName: "javaScript"
            },
            {
              tagId: 5,
              tagName: "javaScript"
            },
            {
              tagId: 6,
              tagName: "javaScript"
            },
            {
              tagId: 7,
              tagName: "javaScript"
            },
            {
              tagId: 8,
              tagName: "javaScript"
            },
            {
              tagId: 9,
              tagName: "javaScript"
            },
            {
              tagId: 10,
              tagName: "javaScript"
            },
            {
              tagId: 11,
              tagName: "javaScript"
            },
            {
              tagId: 12,
              tagName: "javaScript"
            }
          ]
        },
        {
          id: 2,
          title: "中断和中断处理程序",
          abstract: "本次笔记记录了CPU中断是什么？中断类型有哪些？如何设置中断处理程序？本次笔记记录了CPU中断是什么？中断类型有哪些？如何设置中断处理程序？本次笔记记录了CPU中断是什么？中断类型有哪些？如何设置中断处理程序？本次笔记记录了CPU中断是什么？中断类型有哪些？如何设置中断处理程序？",
          author: {
            name: "带ta去蒙古国",
            avatar: "https://pic1.zhimg.com/v2-bb2aa7b20551744a027d8ea9dbcc03c6_xs.jpg"
          },
          viewCount: 10,
          commentCount: 100,
          statCount: 1000,
          tagList: [
            {
              tagId: 1,
              tagName: "javaScript"
            },
            {
              tagId: 2,
              tagName: "javaScript"
            },
            {
              tagId: 3,
              tagName: "javaScript"
            },
            {
              tagId: 4,
              tagName: "javaScript"
            },
            {
              tagId: 5,
              tagName: "javaScript"
            },
            {
              tagId: 6,
              tagName: "javaScript"
            },
            {
              tagId: 7,
              tagName: "javaScript"
            },
            {
              tagId: 8,
              tagName: "javaScript"
            },
            {
              tagId: 9,
              tagName: "javaScript"
            },
            {
              tagId: 10,
              tagName: "javaScript"
            },
            {
              tagId: 11,
              tagName: "javaScript"
            },
            {
              tagId: 12,
              tagName: "javaScript"
            }
          ]
        },
        {
          id: 3,
          title: "中断和中断处理程序",
          abstract: "本次笔记记录了CPU中断是什么？中断类型有哪些？如何设置中断处理程序？本次笔记记录了CPU中断是什么？中断类型有哪些？如何设置中断处理程序？本次笔记记录了CPU中断是什么？中断类型有哪些？如何设置中断处理程序？本次笔记记录了CPU中断是什么？中断类型有哪些？如何设置中断处理程序？",
          author: {
            name: "带ta去蒙古国",
            avatar: "https://pic1.zhimg.com/v2-bb2aa7b20551744a027d8ea9dbcc03c6_xs.jpg"
          },
          viewCount: 10,
          commentCount: 100,
          statCount: 1000,
          tagList: [
            {
              tagId: 1,
              tagName: "javaScript"
            },
            {
              tagId: 2,
              tagName: "javaScript"
            },
            {
              tagId: 3,
              tagName: "javaScript"
            },
            {
              tagId: 4,
              tagName: "javaScript"
            },
            {
              tagId: 5,
              tagName: "javaScript"
            },
            {
              tagId: 6,
              tagName: "javaScript"
            },
            {
              tagId: 7,
              tagName: "javaScript"
            },
            {
              tagId: 8,
              tagName: "javaScript"
            },
            {
              tagId: 9,
              tagName: "javaScript"
            },
            {
              tagId: 10,
              tagName: "javaScript"
            },
            {
              tagId: 11,
              tagName: "javaScript"
            },
            {
              tagId: 12,
              tagName: "javaScript"
            }
          ]
        }
      ],
      questions: [
        {
          id: 1,
          title: "bios如何启动的",
          abstract: "本次笔记记录了CPU中断是什么？中断类型有哪些？如何设置中断处理程序？本次笔记记录了CPU中断是什么？中断类型有哪些？如何设置中断处理程序？本次笔记记录了CPU中断是什么？中断类型有哪些？如何设置中断处理程序？本次笔记记录了CPU中断是什么？中断类型有哪些？如何设置中断处理程序？",
          author: {
            name: "带ta去蒙古国",
            avatar: "https://pic1.zhimg.com/v2-bb2aa7b20551744a027d8ea9dbcc03c6_xs.jpg"
          },
          viewCount: 10,
          commentCount: 100,
          statCount: 1000,
          tagList: [
            {
              tagId: 1,
              tagName: "javaScript"
            },
            {
              tagId: 2,
              tagName: "javaScript"
            },
            {
              tagId: 3,
              tagName: "javaScript"
            },
            {
              tagId: 4,
              tagName: "javaScript"
            },
            {
              tagId: 5,
              tagName: "javaScript"
            },
            {
              tagId: 6,
              tagName: "javaScript"
            },
            {
              tagId: 7,
              tagName: "javaScript"
            },
            {
              tagId: 8,
              tagName: "javaScript"
            },
            {
              tagId: 9,
              tagName: "javaScript"
            },
            {
              tagId: 10,
              tagName: "javaScript"
            },
            {
              tagId: 11,
              tagName: "javaScript"
            },
            {
              tagId: 12,
              tagName: "javaScript"
            }
          ]
        },
        {
          id: 2,
          title: "什么是虚拟内存",
          abstract: "本次笔记记录了CPU中断是什么？中断类型有哪些？如何设置中断处理程序？本次笔记记录了CPU中断是什么？中断类型有哪些？如何设置中断处理程序？本次笔记记录了CPU中断是什么？中断类型有哪些？如何设置中断处理程序？本次笔记记录了CPU中断是什么？中断类型有哪些？如何设置中断处理程序？",
          author: {
            name: "带ta去蒙古国",
            avatar: "https://pic1.zhimg.com/v2-bb2aa7b20551744a027d8ea9dbcc03c6_xs.jpg"
          },
          viewCount: 10,
          commentCount: 100,
          statCount: 1000,
          tagList: [
            {
              tagId: 1,
              tagName: "javaScript"
            },
            {
              tagId: 2,
              tagName: "javaScript"
            },
            {
              tagId: 3,
              tagName: "javaScript"
            },
            {
              tagId: 4,
              tagName: "javaScript"
            },
            {
              tagId: 5,
              tagName: "javaScript"
            },
            {
              tagId: 6,
              tagName: "javaScript"
            },
            {
              tagId: 7,
              tagName: "javaScript"
            },
            {
              tagId: 8,
              tagName: "javaScript"
            },
            {
              tagId: 9,
              tagName: "javaScript"
            },
            {
              tagId: 10,
              tagName: "javaScript"
            },
            {
              tagId: 11,
              tagName: "javaScript"
            },
            {
              tagId: 12,
              tagName: "javaScript"
            }
          ]
        },
        {
          id: 3,
          title: "什么是中断描述符表",
          abstract: "本次笔记记录了CPU中断是什么？中断类型有哪些？如何设置中断处理程序？本次笔记记录了CPU中断是什么？中断类型有哪些？如何设置中断处理程序？本次笔记记录了CPU中断是什么？中断类型有哪些？如何设置中断处理程序？本次笔记记录了CPU中断是什么？中断类型有哪些？如何设置中断处理程序？",
          author: {
            name: "带ta去蒙古国",
            avatar: "https://pic1.zhimg.com/v2-bb2aa7b20551744a027d8ea9dbcc03c6_xs.jpg"
          },
          viewCount: 10,
          commentCount: 100,
          statCount: 1000,
          tagList: [
            {
              tagId: 1,
              tagName: "javaScript"
            },
            {
              tagId: 2,
              tagName: "javaScript"
            },
            {
              tagId: 3,
              tagName: "javaScript"
            },
            {
              tagId: 4,
              tagName: "javaScript"
            },
            {
              tagId: 5,
              tagName: "javaScript"
            },
            {
              tagId: 6,
              tagName: "javaScript"
            },
            {
              tagId: 7,
              tagName: "javaScript"
            },
            {
              tagId: 8,
              tagName: "javaScript"
            },
            {
              tagId: 9,
              tagName: "javaScript"
            },
            {
              tagId: 10,
              tagName: "javaScript"
            },
            {
              tagId: 11,
              tagName: "javaScript"
            },
            {
              tagId: 12,
              tagName: "javaScript"
            }
          ]
        }
      ]
    }
  },
  methods: {
    handleClick(tab, event) {
      console.log(tab, event);
    }
  }
}
</script>

<style scoped>
.el-header {
  display: flex;
  align-items: center;
  padding: 0 7%;
}
.el-main {
  width: 80%;
  margin: 0 auto;
  padding-top: 0;
}

.clearfix:before,
  .clearfix:after {
    display: table;
    content: "";
  }
  .clearfix:after {
    clear: both
  }
.el-card__header {
  padding-top: 0 !important;
}
.wrapper{
    /* background: #cc8548; */
    /* padding: 20px; */
    display: flex;
    flex-direction: row;
    align-items: center; /*垂直居中*/
    justify-content: center; /*水平居中*/
    font-size: 0;
}
.img{
    vertical-align: middle;
    align-items: center;
}
.text{
    flex: 1;
    padding-left: 20px;
    font-size: 16px;
}
</style>