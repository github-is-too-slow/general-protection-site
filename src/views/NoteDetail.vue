<template>
  <el-container>
    <el-header>
      <el-breadcrumb separator="/">
        <el-breadcrumb-item :to="{ path: '/' }">首页</el-breadcrumb-item>
        <el-breadcrumb-item :to="{ path: '/forumDetail/' + forum.id }">{{forum.name}}</el-breadcrumb-item>
        <el-breadcrumb-item><a href="#">{{note.title}}</a></el-breadcrumb-item>
      </el-breadcrumb>
    </el-header>
    <el-main>
      <div class="note-datail-container">
    <el-card class="note-datail-card">
      <h1 class="note-title">{{note.title}}</h1>
      <div class="note-base-info">
        <div class="wrapper">
          <img class="img" style="width: 24px; height: 24px;"
                :src="note.author.avatar">
          <div class="text">{{note.author.name}}</div>
        </div>
        <div class="note-create-time">{{note.createTime}}</div>
        <el-tooltip class="note-count" effect="dark" content="阅读" placement="bottom">
          <span><i class="el-icon-view"></i> {{note.viewCount}}</span>
        </el-tooltip>
        <el-tooltip class="note-count" effect="dark" content="赞" placement="bottom">
          <span><i class="el-icon-thumb"></i> {{note.statCount}}</span>
        </el-tooltip>
        <el-tooltip class="note-count" effect="dark" content="评论" placement="bottom">
          <span><i class="el-icon-s-comment"></i> {{note.commentCount}}</span>
        </el-tooltip>
      </div>
    </el-card>

    <InnerMarkdown :editor="editorWithNoteContent"/>
    <el-card class="note-tool-card">
      <div class="note-tool-box">
        <div class="note-follow-tool">
          <div class="wrapper">
            <img class="img" style="width: 24px; height: 24px;"
                  :src="note.author.avatar">
            <div class="text">{{note.author.name}}</div>
            <el-button round size="mini">关注</el-button>
          </div>
        </div>
        <div class="note-other-tool">
          <el-tooltip class="note-single-tool" effect="dark" content="点赞" placement="top">
            <span><i class="el-icon-thumb"></i> {{note.statCount}}</span>
          </el-tooltip>
          <el-tooltip class="note-single-tool" effect="dark" content="评论" placement="top">
            <span><i class="el-icon-s-comment"></i> {{note.commentCount}}</span>
          </el-tooltip>
          <!-- <el-tooltip class="note-single-tool" effect="dark" content="收藏" placement="bottom">
            <span><i class="el-icon-star-off"></i> {{note.collectCount}}</span>
          </el-tooltip> -->
        </div>
      </div>
    </el-card>
    <div class="comment-area">
      <div class="infinite-list-wrapper" style="overflow:auto">
        <ul
          class="list"
          v-infinite-scroll="load"
          infinite-scroll-disabled="disabled">
          <li v-for="comment in commentList" :key="comment.id" class="comment-list-item">
            <el-image
              class="comment-user-avatar"
              :src="comment.user.avatar"
              fit="fill"></el-image>
            <div class="comment-detail">
              <a href="#" class="comment-user-name">{{comment.user.name}}</a>
              <p class="comment-content">{{comment.content}}</p>
              <div class="comment-tool">
                <span class="time">{{comment.commentTime}}</span>
                <span class="like"><i class="el-icon-thumb"></i> {{comment.starCount}}</span>
                <span class="reply"><i class="el-icon-s-comment"></i> 回复</span>
              </div>
              <div class="childrend-comment-list">
                <div class="childrend-comment-item" v-for="childComment in comment.children" :key="childComment.id">
                  <div class="childrend-comment-item-info">
                    <el-image class="comment-child-user-avatar"
                      :src="childComment.user.avatar"
                      fit="fill"></el-image>
                    <a href="#" class="comment-user-name" style="margin-right: 5px">{{childComment.user.name}}</a>
                    <span class="commented-user-info" v-if="childComment.commentedId != childComment.parentCommentId">回复 {{childComment.commentedUser.name}} ：</span>
                    <span class="comment-content">{{childComment.content}}</span>
                  </div>
                  <div class="comment-tool">
                    <span class="time">{{childComment.commentTime}}</span>
                    <span class="like"><i class="el-icon-thumb"></i> {{childComment.starCount}}</span>
                    <span class="reply"><i class="el-icon-s-comment"></i> 回复</span>
                  </div>
                </div>
              </div>
            </div>
          </li>
        </ul>
        <p v-if="loading">加载中...</p>
        <p v-if="noMore">没有更多了</p>
      </div>
    </div>
  </div>
    </el-main>
  </el-container>

</template>

<script>
import InnerMarkdown from '@/components/InnerMarkdown.vue'
export default {
  name: "NoteDetail",
  components: {
    InnerMarkdown
  },
  data () {
    return {
      commentList: [
        {
          id: 1,
          user: {
            name: "带ta去蒙古国",
            avatar: "https://pic1.zhimg.com/v2-bb2aa7b20551744a027d8ea9dbcc03c6_xs.jpg",
          },
          commentTime: '2021/1/1',
          starCount: 10,
          content: '感谢各位弹幕评论大佬！以下是前后端代码，后端代码中对视频中订单功能mongdb和mysql数据对应不上进行了修改。增加了后台系统订单管理功能，使用容联云进行发送短信，此外还使用了redis集群进行存储，具体参见码云说明~。喜欢的给个Star吧\n~后台代码：https://gitee.com/kimbenzhou/yygh_parent.git\n前台代码：https://gitee.com/kimbenzhou/yygh_admin.git',
          children: [
            {
              id: 111,
              parentCommentId: 1,
              commentedId: 1,
              user: {
                name: "带ta去蒙古国",
                avatar: "https://pic1.zhimg.com/v2-bb2aa7b20551744a027d8ea9dbcc03c6_xs.jpg",
              },
              commentedUser: {
                name: "带ta去蒙古国",
                avatar: "https://pic1.zhimg.com/v2-bb2aa7b20551744a027d8ea9dbcc03c6_xs.jpg",
              },
              commentTime: '2021/1/1',
              starCount: 10,
              content: '感谢各位弹幕评论大佬！以下是前后端代码，后端代码中对视频中订单功能mongdb和mysql数据对应不上进行了修改。增加了后台系统订单管理功能，使用容联云进行发送短信，此外还使用了redis集群进行存储，具体参见码云说明~。喜欢的给个Star吧\n~后台代码：https://gitee.com/kimbenzhou/yygh_parent.git\n前台代码：https://gitee.com/kimbenzhou/yygh_admin.git'
            },
            {
              id: 222,
              parentCommentId: 1,
              commentedId: 2,
              user: {
                name: "带ta去蒙古国",
                avatar: "https://pic1.zhimg.com/v2-bb2aa7b20551744a027d8ea9dbcc03c6_xs.jpg",
              },
              commentedUser: {
                name: "带ta去蒙古国",
                avatar: "https://pic1.zhimg.com/v2-bb2aa7b20551744a027d8ea9dbcc03c6_xs.jpg",
              },
              commentTime: '2021/1/1',
              starCount: 10,
              content: '感谢各位弹幕评论大佬！以下是前后端代码，后端代码中对视频中订单功能mongdb和mysql数据对应不上进行了修改。增加了后台系统订单管理功能，使用容联云进行发送短信，此外还使用了redis集群进行存储，具体参见码云说明~。喜欢的给个Star吧\n~后台代码：https://gitee.com/kimbenzhou/yygh_parent.git\n前台代码：https://gitee.com/kimbenzhou/yygh_admin.git'
            },
            {
              id: 111,
              parentCommentId: 1,
              commentedId: 1,
              user: {
                name: "带ta去蒙古国",
                avatar: "https://pic1.zhimg.com/v2-bb2aa7b20551744a027d8ea9dbcc03c6_xs.jpg",
              },
              commentedUser: {
                name: "带ta去蒙古国",
                avatar: "https://pic1.zhimg.com/v2-bb2aa7b20551744a027d8ea9dbcc03c6_xs.jpg",
              },
              commentTime: '2021/1/1',
              starCount: 10,
              content: '感谢各位弹幕评论大佬！以下是前后端代码，后端代码中对视频中订单功能mongdb和mysql数据对应不上进行了修改。增加了后台系统订单管理功能，使用容联云进行发送短信，此外还使用了redis集群进行存储，具体参见码云说明~。喜欢的给个Star吧\n~后台代码：https://gitee.com/kimbenzhou/yygh_parent.git\n前台代码：https://gitee.com/kimbenzhou/yygh_admin.git'
            },
            {
              id: 222,
              parentCommentId: 1,
              commentedId: 2,
              user: {
                name: "带ta去蒙古国",
                avatar: "https://pic1.zhimg.com/v2-bb2aa7b20551744a027d8ea9dbcc03c6_xs.jpg",
              },
              commentedUser: {
                name: "带ta去蒙古国",
                avatar: "https://pic1.zhimg.com/v2-bb2aa7b20551744a027d8ea9dbcc03c6_xs.jpg",
              },
              commentTime: '2021/1/1',
              starCount: 10,
              content: '感谢各位弹幕评论大佬！以下是前后端代码，后端代码中对视频中订单功能mongdb和mysql数据对应不上进行了修改。增加了后台系统订单管理功能，使用容联云进行发送短信，此外还使用了redis集群进行存储，具体参见码云说明~。喜欢的给个Star吧\n~后台代码：https://gitee.com/kimbenzhou/yygh_parent.git\n前台代码：https://gitee.com/kimbenzhou/yygh_admin.git'
            }
          ]
        },
        {
          id: 1,
          user: {
            name: "带ta去蒙古国",
            avatar: "https://pic1.zhimg.com/v2-bb2aa7b20551744a027d8ea9dbcc03c6_xs.jpg",
          },
          commentTime: '2021/1/1',
          starCount: 10,
          content: '感谢各位弹幕评论大佬！以下是前后端代码，后端代码中对视频中订单功能mongdb和mysql数据对应不上进行了修改。增加了后台系统订单管理功能，使用容联云进行发送短信，此外还使用了redis集群进行存储，具体参见码云说明~。喜欢的给个Star吧\n~后台代码：https://gitee.com/kimbenzhou/yygh_parent.git\n前台代码：https://gitee.com/kimbenzhou/yygh_admin.git',
          children: [
            {
              id: 111,
              parentCommentId: 1,
              commentedId: 1,
              user: {
                name: "带ta去蒙古国",
                avatar: "https://pic1.zhimg.com/v2-bb2aa7b20551744a027d8ea9dbcc03c6_xs.jpg",
              },
              commentedUser: {
                name: "带ta去蒙古国",
                avatar: "https://pic1.zhimg.com/v2-bb2aa7b20551744a027d8ea9dbcc03c6_xs.jpg",
              },
              commentTime: '2021/1/1',
              starCount: 10,
              content: '感谢各位弹幕评论大佬！以下是前后端代码，后端代码中对视频中订单功能mongdb和mysql数据对应不上进行了修改。增加了后台系统订单管理功能，使用容联云进行发送短信，此外还使用了redis集群进行存储，具体参见码云说明~。喜欢的给个Star吧\n~后台代码：https://gitee.com/kimbenzhou/yygh_parent.git\n前台代码：https://gitee.com/kimbenzhou/yygh_admin.git'
            },
            {
              id: 222,
              parentCommentId: 1,
              commentedId: 2,
              user: {
                name: "带ta去蒙古国",
                avatar: "https://pic1.zhimg.com/v2-bb2aa7b20551744a027d8ea9dbcc03c6_xs.jpg",
              },
              commentedUser: {
                name: "带ta去蒙古国",
                avatar: "https://pic1.zhimg.com/v2-bb2aa7b20551744a027d8ea9dbcc03c6_xs.jpg",
              },
              commentTime: '2021/1/1',
              starCount: 10,
              content: '感谢各位弹幕评论大佬！以下是前后端代码，后端代码中对视频中订单功能mongdb和mysql数据对应不上进行了修改。增加了后台系统订单管理功能，使用容联云进行发送短信，此外还使用了redis集群进行存储，具体参见码云说明~。喜欢的给个Star吧\n~后台代码：https://gitee.com/kimbenzhou/yygh_parent.git\n前台代码：https://gitee.com/kimbenzhou/yygh_admin.git'
            },
            {
              id: 111,
              parentCommentId: 1,
              commentedId: 1,
              user: {
                name: "带ta去蒙古国",
                avatar: "https://pic1.zhimg.com/v2-bb2aa7b20551744a027d8ea9dbcc03c6_xs.jpg",
              },
              commentedUser: {
                name: "带ta去蒙古国",
                avatar: "https://pic1.zhimg.com/v2-bb2aa7b20551744a027d8ea9dbcc03c6_xs.jpg",
              },
              commentTime: '2021/1/1',
              starCount: 10,
              content: '感谢各位弹幕评论大佬！以下是前后端代码，后端代码中对视频中订单功能mongdb和mysql数据对应不上进行了修改。增加了后台系统订单管理功能，使用容联云进行发送短信，此外还使用了redis集群进行存储，具体参见码云说明~。喜欢的给个Star吧\n~后台代码：https://gitee.com/kimbenzhou/yygh_parent.git\n前台代码：https://gitee.com/kimbenzhou/yygh_admin.git'
            },
            {
              id: 222,
              parentCommentId: 1,
              commentedId: 2,
              user: {
                name: "带ta去蒙古国",
                avatar: "https://pic1.zhimg.com/v2-bb2aa7b20551744a027d8ea9dbcc03c6_xs.jpg",
              },
              commentedUser: {
                name: "带ta去蒙古国",
                avatar: "https://pic1.zhimg.com/v2-bb2aa7b20551744a027d8ea9dbcc03c6_xs.jpg",
              },
              commentTime: '2021/1/1',
              starCount: 10,
              content: '感谢各位弹幕评论大佬！以下是前后端代码，后端代码中对视频中订单功能mongdb和mysql数据对应不上进行了修改。增加了后台系统订单管理功能，使用容联云进行发送短信，此外还使用了redis集群进行存储，具体参见码云说明~。喜欢的给个Star吧\n~后台代码：https://gitee.com/kimbenzhou/yygh_parent.git\n前台代码：https://gitee.com/kimbenzhou/yygh_admin.git'
            }
          ]
        },
        {
          id: 1,
          user: {
            name: "带ta去蒙古国",
            avatar: "https://pic1.zhimg.com/v2-bb2aa7b20551744a027d8ea9dbcc03c6_xs.jpg",
          },
          commentTime: '2021/1/1',
          starCount: 10,
          content: '感谢各位弹幕评论大佬！以下是前后端代码，后端代码中对视频中订单功能mongdb和mysql数据对应不上进行了修改。增加了后台系统订单管理功能，使用容联云进行发送短信，此外还使用了redis集群进行存储，具体参见码云说明~。喜欢的给个Star吧\n~后台代码：https://gitee.com/kimbenzhou/yygh_parent.git\n前台代码：https://gitee.com/kimbenzhou/yygh_admin.git',
          children: [
            {
              id: 111,
              parentCommentId: 1,
              commentedId: 1,
              user: {
                name: "带ta去蒙古国",
                avatar: "https://pic1.zhimg.com/v2-bb2aa7b20551744a027d8ea9dbcc03c6_xs.jpg",
              },
              commentedUser: {
                name: "带ta去蒙古国",
                avatar: "https://pic1.zhimg.com/v2-bb2aa7b20551744a027d8ea9dbcc03c6_xs.jpg",
              },
              commentTime: '2021/1/1',
              starCount: 10,
              content: '感谢各位弹幕评论大佬！以下是前后端代码，后端代码中对视频中订单功能mongdb和mysql数据对应不上进行了修改。增加了后台系统订单管理功能，使用容联云进行发送短信，此外还使用了redis集群进行存储，具体参见码云说明~。喜欢的给个Star吧\n~后台代码：https://gitee.com/kimbenzhou/yygh_parent.git\n前台代码：https://gitee.com/kimbenzhou/yygh_admin.git'
            },
            {
              id: 222,
              parentCommentId: 1,
              commentedId: 2,
              user: {
                name: "带ta去蒙古国",
                avatar: "https://pic1.zhimg.com/v2-bb2aa7b20551744a027d8ea9dbcc03c6_xs.jpg",
              },
              commentedUser: {
                name: "带ta去蒙古国",
                avatar: "https://pic1.zhimg.com/v2-bb2aa7b20551744a027d8ea9dbcc03c6_xs.jpg",
              },
              commentTime: '2021/1/1',
              starCount: 10,
              content: '感谢各位弹幕评论大佬！以下是前后端代码，后端代码中对视频中订单功能mongdb和mysql数据对应不上进行了修改。增加了后台系统订单管理功能，使用容联云进行发送短信，此外还使用了redis集群进行存储，具体参见码云说明~。喜欢的给个Star吧\n~后台代码：https://gitee.com/kimbenzhou/yygh_parent.git\n前台代码：https://gitee.com/kimbenzhou/yygh_admin.git'
            },
            {
              id: 111,
              parentCommentId: 1,
              commentedId: 1,
              user: {
                name: "带ta去蒙古国",
                avatar: "https://pic1.zhimg.com/v2-bb2aa7b20551744a027d8ea9dbcc03c6_xs.jpg",
              },
              commentedUser: {
                name: "带ta去蒙古国",
                avatar: "https://pic1.zhimg.com/v2-bb2aa7b20551744a027d8ea9dbcc03c6_xs.jpg",
              },
              commentTime: '2021/1/1',
              starCount: 10,
              content: '感谢各位弹幕评论大佬！以下是前后端代码，后端代码中对视频中订单功能mongdb和mysql数据对应不上进行了修改。增加了后台系统订单管理功能，使用容联云进行发送短信，此外还使用了redis集群进行存储，具体参见码云说明~。喜欢的给个Star吧\n~后台代码：https://gitee.com/kimbenzhou/yygh_parent.git\n前台代码：https://gitee.com/kimbenzhou/yygh_admin.git'
            },
            {
              id: 222,
              parentCommentId: 1,
              commentedId: 2,
              user: {
                name: "带ta去蒙古国",
                avatar: "https://pic1.zhimg.com/v2-bb2aa7b20551744a027d8ea9dbcc03c6_xs.jpg",
              },
              commentedUser: {
                name: "带ta去蒙古国",
                avatar: "https://pic1.zhimg.com/v2-bb2aa7b20551744a027d8ea9dbcc03c6_xs.jpg",
              },
              commentTime: '2021/1/1',
              starCount: 10,
              content: '感谢各位弹幕评论大佬！以下是前后端代码，后端代码中对视频中订单功能mongdb和mysql数据对应不上进行了修改。增加了后台系统订单管理功能，使用容联云进行发送短信，此外还使用了redis集群进行存储，具体参见码云说明~。喜欢的给个Star吧\n~后台代码：https://gitee.com/kimbenzhou/yygh_parent.git\n前台代码：https://gitee.com/kimbenzhou/yygh_admin.git'
            }
          ]
        },
        {
          id: 1,
          user: {
            name: "带ta去蒙古国",
            avatar: "https://pic1.zhimg.com/v2-bb2aa7b20551744a027d8ea9dbcc03c6_xs.jpg",
          },
          commentTime: '2021/1/1',
          starCount: 10,
          content: '感谢各位弹幕评论大佬！以下是前后端代码，后端代码中对视频中订单功能mongdb和mysql数据对应不上进行了修改。增加了后台系统订单管理功能，使用容联云进行发送短信，此外还使用了redis集群进行存储，具体参见码云说明~。喜欢的给个Star吧\n~后台代码：https://gitee.com/kimbenzhou/yygh_parent.git\n前台代码：https://gitee.com/kimbenzhou/yygh_admin.git',
          children: [
            {
              id: 111,
              parentCommentId: 1,
              commentedId: 1,
              user: {
                name: "带ta去蒙古国",
                avatar: "https://pic1.zhimg.com/v2-bb2aa7b20551744a027d8ea9dbcc03c6_xs.jpg",
              },
              commentedUser: {
                name: "带ta去蒙古国",
                avatar: "https://pic1.zhimg.com/v2-bb2aa7b20551744a027d8ea9dbcc03c6_xs.jpg",
              },
              commentTime: '2021/1/1',
              starCount: 10,
              content: '感谢各位弹幕评论大佬！以下是前后端代码，后端代码中对视频中订单功能mongdb和mysql数据对应不上进行了修改。增加了后台系统订单管理功能，使用容联云进行发送短信，此外还使用了redis集群进行存储，具体参见码云说明~。喜欢的给个Star吧\n~后台代码：https://gitee.com/kimbenzhou/yygh_parent.git\n前台代码：https://gitee.com/kimbenzhou/yygh_admin.git'
            },
            {
              id: 222,
              parentCommentId: 1,
              commentedId: 2,
              user: {
                name: "带ta去蒙古国",
                avatar: "https://pic1.zhimg.com/v2-bb2aa7b20551744a027d8ea9dbcc03c6_xs.jpg",
              },
              commentedUser: {
                name: "带ta去蒙古国",
                avatar: "https://pic1.zhimg.com/v2-bb2aa7b20551744a027d8ea9dbcc03c6_xs.jpg",
              },
              commentTime: '2021/1/1',
              starCount: 10,
              content: '感谢各位弹幕评论大佬！以下是前后端代码，后端代码中对视频中订单功能mongdb和mysql数据对应不上进行了修改。增加了后台系统订单管理功能，使用容联云进行发送短信，此外还使用了redis集群进行存储，具体参见码云说明~。喜欢的给个Star吧\n~后台代码：https://gitee.com/kimbenzhou/yygh_parent.git\n前台代码：https://gitee.com/kimbenzhou/yygh_admin.git'
            },
            {
              id: 111,
              parentCommentId: 1,
              commentedId: 1,
              user: {
                name: "带ta去蒙古国",
                avatar: "https://pic1.zhimg.com/v2-bb2aa7b20551744a027d8ea9dbcc03c6_xs.jpg",
              },
              commentedUser: {
                name: "带ta去蒙古国",
                avatar: "https://pic1.zhimg.com/v2-bb2aa7b20551744a027d8ea9dbcc03c6_xs.jpg",
              },
              commentTime: '2021/1/1',
              starCount: 10,
              content: '感谢各位弹幕评论大佬！以下是前后端代码，后端代码中对视频中订单功能mongdb和mysql数据对应不上进行了修改。增加了后台系统订单管理功能，使用容联云进行发送短信，此外还使用了redis集群进行存储，具体参见码云说明~。喜欢的给个Star吧\n~后台代码：https://gitee.com/kimbenzhou/yygh_parent.git\n前台代码：https://gitee.com/kimbenzhou/yygh_admin.git'
            },
            {
              id: 222,
              parentCommentId: 1,
              commentedId: 2,
              user: {
                name: "带ta去蒙古国",
                avatar: "https://pic1.zhimg.com/v2-bb2aa7b20551744a027d8ea9dbcc03c6_xs.jpg",
              },
              commentedUser: {
                name: "带ta去蒙古国",
                avatar: "https://pic1.zhimg.com/v2-bb2aa7b20551744a027d8ea9dbcc03c6_xs.jpg",
              },
              commentTime: '2021/1/1',
              starCount: 10,
              content: '感谢各位弹幕评论大佬！以下是前后端代码，后端代码中对视频中订单功能mongdb和mysql数据对应不上进行了修改。增加了后台系统订单管理功能，使用容联云进行发送短信，此外还使用了redis集群进行存储，具体参见码云说明~。喜欢的给个Star吧\n~后台代码：https://gitee.com/kimbenzhou/yygh_parent.git\n前台代码：https://gitee.com/kimbenzhou/yygh_admin.git'
            }
          ]
        }
      ],
      count: 10,
      loading: false,
      forum: {
        id: 1,
        name: '操作系统真相还原',
      },
      note: {
        id: 1,
        title: '每日算法&面试题⚡动态规划21天——第二天',
        author: {
          name: "带ta去蒙古国",
          avatar: "https://pic1.zhimg.com/v2-bb2aa7b20551744a027d8ea9dbcc03c6_xs.jpg"
        },
        createTime: "2021-1-1",
        viewCount: 10,
        commentCount: 100,
        statCount: 1000,
        content: "## 这是一个二级标题\n### 这是一个三级标题\n#### 这是一个四级标题数组的每个下标作为一个阶梯，第 i 个阶梯对应着一个非负数的体力花费值 cost[i]（下标从 0 开始）。每当你爬上一个阶梯你都要花费对应的体力值，一旦支付了相应的体力值，你就可以选择向上爬一个阶梯或者爬两个阶梯。请你找出达到楼层顶部的最低花费。在开始时，你可以选择从下标为 0 或 1 的元素作为初始阶梯。"
      },
      defaultEditor: {
        style: "",
        value: "",
        toolbarsBackground: "#292d38",
        subfield: false,
        default_open: "preview",
        tabSize: 4,
        editable: false,
        toolbarsFlag: false ,
        toolbars: {
          bold: true, // 粗体
          italic: true, // 斜体
          header: true, // 标题
          underline: true, // 下划线
          strikethrough: true, // 中划线
          mark: true, // 标记
          superscript: true, // 上角标
          subscript: true, // 下角标
          quote: true, // 引用
          ol: true, // 有序列表
          ul: true, // 无序列表
          link: true, // 链接
          imagelink: true, // 图片链接
          code: true, // code
          table: true, // 表格
          fullscreen: true, // 全屏编辑
          readmodel: true, // 沉浸式阅读
          htmlcode: true, // 展示html源码
          help: true, // 帮助
          /* 1.3.5 */
          undo: true, // 上一步
          redo: true, // 下一步
          trash: true, // 清空
          save: true, // 保存（触发events中的save事件）
          /* 1.4.2 */
          navigation: true, // 导航目录
          /* 2.1.8 */
          alignleft: true, // 左对齐
          aligncenter: true, // 居中
          alignright: true, // 右对齐
          /* 2.2.1 */
          subfield: true, // 单双栏模式
          preview: true, // 预览
        }
      }
    }
  },
  computed: {
    editorWithNoteContent(){
      this.defaultEditor.value = this.note.content;
      return this.defaultEditor;
    },
    noMore () {
      return this.count >= 200
    },
    disabled () {
      // return this.loading || this.noMore
      return true;
    }
  },
  methods: {
    load () {
      this.loading = true
      setTimeout(() => {
        this.count += 2
        this.loading = false
      }, 1000)
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
/* .note-datail-container {
  width: 80%;
  margin: 0 auto;
} */
.note-datail-card {
  margin-bottom: 20px;
}
.note-title {
  font-size: 28px;
  color: #222226;
  font-weight: 600;
  line-height: 1.5;
  margin: 0;
}
.note-base-info {
  display: flex;
  justify-content: flex-start;
  align-items: center;
}
.note-tool-box {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.wrapper{
    /* background: #cc8548; */
    /* padding: 20px; */
    display: flex;
    flex-direction: row;
    align-items: center; /*垂直居中*/
    justify-content: flex-start; /*水平居中*/
    font-size: 0;
}
.img{
    vertical-align: middle;
    align-items: center;
}
.text{
    padding: 0 5px;
    font-size: 12px;
}
.note-create-time, .note-count, .note-single-tool {
  font-size: 12px;
  margin-left: 20px;
}
.comment-area {
  margin: 30px;
}
.comment-list-item {
  display: flex;
}
.comment-list-item .comment-detail {
  flex: 1;
}
.comment-user-avatar {
  width: 48px;
  height: 48px;
  border-radius: 24px;
  margin: 0 10px;
}
.comment-child-user-avatar {
  width: 24px;
  height: 24px;
  border-radius: 24px;
  margin-right: 5px;
}
.comment-content {
  line-height: 20px;
  padding: 2px 0;
  font-size: 14px;
  font-weight: 400;
  text-shadow: none;
  overflow: hidden;
  word-wrap: break-word;
  word-break: break-word;
  white-space: pre-wrap;
}
.time, .like, .reply {
  color: #99a2aa;
  line-height: 14px;
  margin-top: 6px;
  margin-right: 20px;
  font-size: 12px;
}
.childrend-comment-item {
  margin: 10px 0;
}
.childrend-comment-item-info {
  display: flex;
  justify-content: flex-start;
  align-items: center;
  flex-wrap: wrap;
}
</style>