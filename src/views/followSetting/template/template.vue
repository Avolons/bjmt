<style lang="less">
.line {
	padding: 5px 20px;
	border-bottom: 1px solid #2d8cf0;
	width: 100%;
	margin-bottom: 34px;
	h2 {
		font-weight: 400;
		font-family: "Open Sans", "Helvetica Neue", Helvetica, Arial, sans-serif;
		font-size: 22px;
	}
}

.lineheight32 {
	line-height: 32px;
}

.mb5 {
	margin-bottom: 5px;
}

.padleft40 {
	padding-left: 40px;
}

.margintop20 {
	margin-top: 20px;
}

.border1 {
	border: 1px #b1b1b1 solid;
}

.template {
	/* background: #fff; */
	height: 100%;
	color: #333;
	form {
		padding-right: 500px;
		&:after {
			content: "";
			display: block;
			clear: both;
		}
		.ivu-form-item:nth-of-type(1),
		.ivu-form-item:nth-of-type(6) {
			width: 100%;
		}
		.ivu-form-item:nth-of-type(7) {
			.ivu-input-wrapper {
				width: 60%;
			}
		}
		.ivu-form-item:nth-of-type(7) {
			.ivu-input-wrapper {
				width: 60%;
			}
		}
		.ivu-form-item {
			width: 50%;
			float: left;
		}
	}
	.questionTem {
		background: #fff;
		.setQuestion {
			padding: 0 200px;
			.questionList {
				height: 100%;
			}
			.questionSelect {
				height: 100%; // border-left: 1px #b1b1b1 solid;
				p {
					line-height: 40px;
					font-size: 22px;
				}
			}
		}
	}
}

.collapseStyle {
	border: 0;
}

.ivu-timeline-item-content {
	border: 1px solid #dddee1;
}

.ivu-tabs-bar {
	padding: 0 10px;
}

.template {
	&_main {
		&_commonTitle {
			font-size: 13px;
			margin: 15px 0;
			>span {
				display: inline-block;
				height: 25px;
				line-height: 25px;
				width: 25px;
				border-radius: 50%;
				background-color: #2d8cf0;
				text-align: center;
				color: #fff;
				margin-right: 10px;
			}
		}
		&_stepOne {
			max-width: 900px;
		}
		&_tag {
			border: 1px solid #dadada;
			height: 200px;
			border-radius: 5px;
			.ivu-tabs-bar {
				margin: 0;
			}
			.ivu-tabs-content-animated {
				height: calc(~'100% - 36px');
				.ivu-tabs-tabpane {
					height: 100%;
					overflow-y: auto;
				}
			}
		}
		&_tagList {
			>li {
				margin: 5px;
				border-radius: 5px;
				padding: 1px 10px;
				cursor: pointer;
				background-color: #f3f3f3;
			}
		}
		&_disAdd {
			width: 50%;
		}
		&_questionItem {
			background-color: #fff;
			border-radius: 5px;
			box-sizing: border-box;
			padding: 10px;
			border: 1px solid #dadada;
			margin-bottom: 10px;
			h3 {
				font-size: 13px;
				background-color: #f1f1f1;
				border-radius: 5px;
				padding: 5px 15px;
				color: #2d8cf0;
				margin: 15px 0;
			}
		}
		&_questionSelect {
			border-radius: 5px;
			box-sizing: border-box;
		}
		&_questList {
			border: 1px solid #dadada;
			background-color: #f3f3f3;
			border-radius: 5px;
			max-height: 500px;
			overflow-y: auto;
			box-sizing: border-box;
			padding: 10px;
			.isClick {
				background-color: #dadada;
			}
			>li {
				height: 30px;
				line-height: 30px;
				text-align: left;
				background-color: #2d8cf0;
				color: #fff;
				font-size: 13px;
				border-radius: 5px;
				margin-bottom: 10px;
				.ivu-poptip {
					width: 100%;
					cursor: pointer;
					.ivu-poptip-rel {
						width: 100%;
					}
				}
				.ivu-btn-text {
					color: #fff;
					text-align: left;
					display: block;
					margin-left: 30px;
					width: calc(~"100% - 30px")
				}
			}
		}
	}
}
</style>
<template>
	<Row class="template">
		<Card>
			<p slot="title">
				<Icon type="social-buffer"></Icon>
				随访模板信息
			</p>
			<Form ref="templateForm" :model="templateForm" :rules="ruleValidate" :label-width="80">
				<FormItem label="模板名称" prop="name">
					<Input v-model="templateForm.name" placeholder="请填写模板名称"></Input>
				</FormItem>
				<FormItem label="疾病类型">
					<Select :label="labelobj" v-model="templateForm.diseaseId" multiple filterable remote not-found-text="" :remote-method="remoteMethod">
						<Option v-for="(item, index) in diseaseList" :value="item.value" :key="item.value">{{item.label}}</Option>
					</Select>
				</FormItem>
				<FormItem label="静默时间" prop="silencetime">
					<InputNumber v-model="templateForm.silencetime" :min="0" style="width:100%;" placeholder="请输入静默时间,类型为数字,单位默认为秒"></InputNumber>
					<!-- <Input v-model="templateForm.silencetime" placeholder="Enter your name"></Input> -->
				</FormItem>
				<FormItem label="重复次数" prop="outrepeattimes">
					<InputNumber v-model="templateForm.outrepeattimes" :min="0" style="width:100%;" placeholder="请输入重复次数,类型为数字,单位默认为次数"></InputNumber>
					<!-- <Input v-model="templateForm.outrepeattimes" placeholder="Enter your name"></Input> -->
				</FormItem>
				<FormItem label="起始问题" prop="firsttaskid">
					<InputNumber v-model="templateForm.firsttaskid" :min="1000" style="width:100%;" placeholder="请输入重复次数,类型为数字,单位默认为次数"></InputNumber>
					<!-- <Input v-model="templateForm.firsttaskid" placeholder="Enter your name"></Input> -->
				</FormItem>
				<FormItem label="合成声音" prop="person">
					<RadioGroup v-model="templateForm.person" @on-change="radioChange">
						<Radio label="0">女声</Radio>
						<Radio label="1">男声</Radio>
					</RadioGroup>
				</FormItem>
				<FormItem label="添加通用库" prop="addSubmoulds">
					<Input v-model="templateForm.addSubmoulds" placeholder="请添加以.xml结尾的文件"></Input>
					<Button type="primary" @click="addTag">添加</Button>
				</FormItem>
				<FormItem label="通用库">
					<tag v-for="item in tagCount" color="blue" :key="item" :name="item" closable @on-close="tagClose">{{item}}</tag>
				</FormItem>
			</Form>
		</Card>
		<Card style="margin-top:10px">
			<p slot="title">
				<Icon type="android-list"></Icon>
				配置随访问题
			</p>
			<Row :gutter="20">
				<Col span="10">
				<div class="template_main_stepOne">
					<h3 class="template_main_commonTitle">
						<span>1</span>
						选择疾病类型
					</h3>
					<Alert type="success">
						添加疾病类型显示对应的指标
					</Alert>
					<div class="template_main_disAdd">
						<Select placeholder="选择疾病类型获取对应的指标" v-model="listDisID" filterable remote not-found-text="" :remote-method="remoteMethod_else" clearable @on-change="selectChange">
							<Option v-for="option in diseaseListQues" :value="option.value" :key="option.value">{{option.label}}</Option>
						</Select>
					</div>
				</div>
				</Col>
				<Col span="14">
				<div class="template_main_stepOne">
					<h3 class="template_main_commonTitle">
						<span>2</span>
						配置问题
					</h3>
					<Alert type="success">
						双击指标可添加到第三步
					</Alert>
					<Row class="targetpz margintop20">
						<Tabs value="1" class="template_main_tag" @on-click="tabsClick">
							<template v-for="item,index in questionList">
								<TabPane :label="item.label" :name="index+1+''">
									<ul class="template_main_tagList">
										<li v-for="ite in item.list">
											<Button type="text" v-on:dblclick.native="addQuestion(ite)">{{ite.title}}</Button>
										</li>
									</ul>
								</TabPane>
							</template>
						</Tabs>
					</Row>
				</div>
				</Col>
			</Row>
		</Card>
		<Card style="margin-top:10px">
			<p slot="title">
				<Icon type="android-archive"></Icon>
				随访方案基本信息
			</p>
			<Alert type="success">
				双击问题可添加到右侧进行编辑
			</Alert>
			<Row class="setQuestion" :gutter="20">
				<Col span="6" class="questionList">
				<ul class="template_main_questList">
					<li :class="{'isClick':item.isClick==1}" v-for="item in this.stepThirdQuestion">
						<Poptip trigger="hover" title="" content="双击问题开始编辑">
							<Button type="text" v-on:dblclick.native="addThirdQuestion(item)">{{item.title}}</Button>
						</Poptip>
					</li>
				</ul>
				<p style="line-height: 30px;">小提示：补充完右侧末班内容后，点击创建即可新增模板！</p>
				<Button type="primary" @click="addTemplate(0)">保存随访模板</Button>
				<Button type="info" @click="addTemplate(1)">另存为新模板</Button>
				</Col>
				<Col span="18" class="template_main_questionSelect">
				<div class="template_main_questionItem" v-for="(item, index) in this.templateList" :key="item.questionIdXml">
					<Row>
						<Col span="2">
						<div style="border-radius: 100%; width: 38px; height: 38px; line-height: 38px; text-align: center;background:#2d8cf0;color:#fff">{{item.questionIdXml}}</div>
						</Col>
						<Col span="18">
						<Collapse v-model="collapse" class="collapseStyle">
							<Panel :name="index+1+''">
								{{item.questionName}}
								<ul slot="content" v-for="item1 in item.questionTempleQuestionJumps">
									<li>
										<Row class="itemli">
											<h3 class="">处理: {{item1.switchId==-1?"无匹配":item1.switchId==-2?"无声音":item1.switchId==-3?"通用处理":item1.switchId}}</h3>
											<Row class="padleft40 mb5" v-show="item1.switchText">
												<Col span="4" style="width:105px" class="lineheight32">话术名称:</Col>
												<Col span="20" style="width:calc(100% - 105px)" class="lineheight32">
												<span>{{item1.switchText}}</span>
												</Col>
											</Row>
											<Row class="padleft40 mb5" v-show="item1.switchRegexText">
												<Col span="4" style="width:105px" class="lineheight32">判别规则:</Col>
												<Col span="20" style="width:calc(100% - 105px)" class="lineheight32">
												<span>{{item1.switchRegexText}}</span>
												</Col>
											</Row>
											<Row class="padleft40 mb5" v-show="item1.keyname">
												<Col span="4" style="width:105px" class="lineheight32">指标名称/值：</Col>
												<Col span="20" style="width:calc(100% - 105px)" class="lineheight32">
												<span>{{item1.keyname}} / {{item1.keyvalue}}</span>
												</Col>
											</Row>
											<Row class="padleft40 mb5">
												<Col span="4" style="width:105px" class="lineheight32">跳转问题编号:</Col>
												<Col span="20" style="width:calc(100% - 105px)" class="textCenter">
												<Input placeholder="请填写跳转问题编号" v-model="item1.nextQuestionId"></Input>
												</Col>
											</Row>
											<Row class="padleft40 mb5" v-if="item1.switchId==-1">
												<Col span="4" style="width:105px" class="lineheight32">无匹配超次数跳转:</Col>
												<Col span="18" style="width:calc(100% - 105px)" class="textCenter">
												<Input placeholder="请填写无匹配超次数跳转" v-model="item1.outRptSwitchID"></Input>
												</Col>
											</Row>
										</Row>
									</li>
								</ul>
							</Panel>
						</Collapse>
						</Col>
						<Col span="4" style="height:38px">
						<Button type="primary" @click.native="update(item)" size="small" style="margin-top:7px;margin-left:10px">更新</Button>
						<Button type="warning" @click.native="deleteCol(index,item.questionId)" size="small" style="margin-top:7px;margin-left:10px">删除</Button>
						</Col>
					</Row>
				</div>
				</Col>
			</Row>
		</Card>
	</Row>
</template>

<script>
import { API } from '@/services';
export default {

	data() {
		return {
			playWavOnly: 0,//是否是纯放音
			labelobj: [],
			templateId: '',//模板id
			/* 模板默认信息 */
			templateForm: {
				name: '',//模板名称
				diseaseId: [],//疾病类型
				silencetime: 5,//静默时间
				outrepeattimes: 3,//重复次数
				firsttaskid: 1000,//起始问题
				person: '0',//合成声音
				addSubmoulds: ""//添加的通用库
			},
			listDisID: "",//第二部被选中的疾病的id
			tagCount: [],//通用库
			/* 验证规则 */
			ruleValidate: {
				name: [
					{ required: true, message: '模板名称不能为空', trigger: 'blur' }
				],
				silencetime: [
					{ required: true, message: '静默时间不能为空', trigger: 'blur' }
				],
			},
			diseaseListQues: [],//问题编辑情况下的远程搜索疾病列表
			diseaseList: [],//远程搜索疾病列表
			switchArr: [],//语音list
			templateList: [],//模板语音开场白
			questionList: [{
				label: "无",
				list: [],
				isGet: false,
			}, {
				label: "症状",
				list: [],
				isGet: false,
			}, {
				label: "体征",
				list: [],
				isGet: false,
			}, {
				label: "生活方式指导",
				list: [],
				isGet: false,
			}, {
				label: "辅助检查",
				list: [],
				isGet: false,
			}, {
				label: "用药反馈",
				list: [],
				isGet: false,
			}, {
				label: "转诊情况",
				list: [],
				isGet: false,
			}, {
				label: "通用",
				list: [],
				isGet: false,
			}],//问题总列表
			stepThirdQuestion: [],//第三步配置问题
			selecetDiseId: '',//第二部选中的疾病类型的id
			collapse: '1',
			showRow: false,
			lastQuestionId: '',//最后一个问题的索引
			resDislist: []
		}
	},
	created() {
		this.fetchData();
	},
	mounted() {
		if (this.templateId != 'new') {
			this.templateInfo();
			this.templateResolve();
		}
	},
	methods: {
		/** 
		 * 更新问题
		 */
		update(quesobj){
			this.$Spin.show();
			API.voiceSetting.question({
				questionId: quesobj.questionId
			}).then((res) => {
				let saveSwitch = res.data;//临时数据
				if(saveSwitch.length>0){
					quesobj.questionName=saveSwitch[0].questionName;
				}
				let newdata=[];
				newdata.push(
					{
						switchId: -1,
						questionIdXml:quesobj.questionIdXml
					}, {
						switchId: -2,
						questionIdXml:quesobj.questionIdXml
					}, {
						switchId: -3,
						questionIdXml:quesobj.questionIdXml
					});
			
				saveSwitch.forEach((item) => {
					newdata.push({
						switchText: item.switchText,
						switchId: item.switchId || item.switchID,
						switchRegexText: item.switchRegexText,
						keyname: item.keyname,
						outRptSwitchID: item.outRptSwitchID,
						keyvalue: item.keyvalue,
						questionIdXml:quesobj.questionIdXml
					}
					)
				})
				for (const item of newdata) {
					for (const ite of quesobj.questionTempleQuestionJumps) {
						if(item.switchId==ite.switchId){
							item.outRptSwitchID=ite.outRptSwitchID;
							item.nextQuestionId=ite.nextQuestionId;
						}
					}
				}

				quesobj.questionTempleQuestionJumps=newdata;
				this.$Spin.hide();
			}).catch((error) => {

			})
		},
		/*
		*获取模板id
		*/
		fetchData() {
			this.templateId = this.$route.params.id
		},
		/*
		*通过模板id获取模板表单信息
		*/
		templateInfo() {
			API.followTemplate.editList({
				id: this.templateId,
			}).then((res) => {
				/** 
				 * 基本信息赋值
				 */
				res.data.diseaseId = res.data.diseaseId.split(",");
				res.data.diseaseName = res.data.diseaseName.split(",");
				this.diseaseList = [];
				this.labelobj = [];
				res.data.diseaseName.forEach((item, index) => {
					this.diseaseList.push({
						label: item,
						value: res.data.diseaseId[index]
					})
					this.labelobj.push(item);
				})
				this.templateForm = {
					name: res.data.name,
					silencetime: res.data.silencetime - 0,
					outrepeattimes: res.data.outrepeattimes - 0,
					firsttaskid: res.data.firsttaskid - 0,
					person: res.data.person,
					diseaseId: res.data.diseaseId,
					addSubmoulds: ''//添加的通用库
				}
				/** 
				 * 通用库赋值
				 */
				this.tagCount = res.data.submoulds ? res.data.submoulds.split(';') : [];

			}).catch((error) => {
				console.log(error)
			})
		},
		/*
		*通过模板id获取模板处理信息
		*/
		templateResolve() {
			API.followTemplate.questionList({
				id: this.templateId,
			}).then((res) => {
				let maps = {
					questionId: '',
					questionIdXml: '',
					targetId: '',
					questionTempleQuestionJumps: []
				}
				res.data.forEach((item) => {
					this.stepThirdQuestion.push({
						title: item.questionName,
						id: item.questionId,
					})
					this.templateList.push({
						questionId: item.questionId,
						questionIdXml: item.questionIdXml,
						targetId: item.targetId,
						questionName: item.questionName,
						questionTempleQuestionJumps: item.questionTempleQuestionJumps
					})
				})

			}).catch((error) => {
				console.log(error)
			})
		},
		/*
		*监听radio男声女声
		*/
		radioChange(value) {
			this.person = value;
		},
		/*
		* 通用库添加标签
		*/
		addTag() {
			let flag = 0;
			this.tagCount.forEach((item) => {
				if (this.templateForm.addSubmoulds == item || this.templateForm.addSubmoulds == '') {
					flag++;
					this.$Message.warning('您添加的格式不正确或者重复添加');
				}
			})
			if (flag > 0) {
				this.templateForm.addSubmoulds = ''
				return false;
			}
			let strRegex = /.\.xml/; //用于验证图片扩展名的正则表达式
			let re = new RegExp(strRegex);
			if (re.test(this.templateForm.addSubmoulds)) {
				/** 
				 * 验证通过
				 */
				this.tagCount.push(this.templateForm.addSubmoulds)
				this.templateForm.addSubmoulds = '';
			} else {
				this.$Message.warning("请添加以.xml结尾的文件")
			}
		},
		/*
		*删除标签
		*/
		tagClose(event, name) {
			const index = this.tagCount.indexOf(name);
			this.tagCount.splice(index, 1);
		},
		/** 
		 * 自动完成
		 */
		remoteMethod(query) {
			if (query == '') {
				return false;
			}
			this.diseaseList = [];
			API.followProblems.disease({
				zjm: query
			}).then((res) => {
				let parr = [];
				(res.data).forEach((item) => {
					parr.push({
						value: item.id,
						label: item.value
					})
				})
				this.diseaseList = parr;
			}).catch((error) => {
				console.log(error)
			})
		},
		/*
		*疾病类型--远程搜索
		*/
		remoteMethod_else(query) {
			if (query.trim() == '') {
				for (let item of this.questionList) {
					item.list=[];
					item.isGet=false;
				}
				return false;
			}
			this.listDisID = '';
			this.diseaseListQues = [];
			API.followProblems.disease({
				zjm: query
			}).then((res) => {
				let parr = [];
				(res.data).forEach((item) => {
					parr.push({
						value: item.id,
						label: item.value
					})
				})
				this.diseaseListQues = parr;
			}).catch((error) => {
				console.log(error)
			})
		},
		/*
		*获取选中的疾病类型id，根据疾病类型获取所有问题
		*/
		selectChange(value) {
			this.selecetDiseId = value;
			if (value !== '') {
				API.followProblems.list({
					pager: 1,
					limit: 1000,
					title: '',
					diseaseId: value
				}).then((res) => {
					this.questionList[0].list=res.data;
					this.questionList[0].isGet=true;
				}).catch((error) => {
					console.log(error)
				})
			} else {
				for (let item of this.questionList) {
					item.list=[];
					item.isGet=false;
				}
			}

		},
		/*
		*双击添加事件
		*/
		addQuestion(item) {
			this.stepThirdQuestion.push(item);
		},
		/*
		*第三步点击问题开始编辑
		*/
		addThirdQuestion(item) {
			if (item.isClick == 1) {
				return false;
			}
			/** 
			 * 获取问题列表编号
			 */
			let questionIdXml = 1000;
			questionIdXml = questionIdXml + this.templateList.length;
			/** 
			 * 根据问题id获取问题列表
			 */
			API.voiceSetting.question({
				questionId: item.id
			}).then((res) => {
				item.isClick = 1;
				let saveSwitch = res.data;//临时数据
				/** 
				 * 临时数据初始化三种问题
				 */
				/* if(item.playWavOnly==0){ */
				this.switchArr.push(
					{
						switchId: -1,
						questionIdXml: questionIdXml,
					}, {
						switchId: -2,
						questionIdXml: questionIdXml,
					}, {
						switchId: -3,
						questionIdXml: questionIdXml,
					});
				/* } */
				/** 
				 * 遍历生成新的问题模板
				 */
				saveSwitch.forEach((item) => {
					this.switchArr.push({
						switchText: item.switchText,
						switchId: item.switchId || item.switchID,
						switchRegexText: item.switchRegexText,
						keyname: item.keyname,
						outRptSwitchID: item.outRptSwitchID,
						keyvalue: item.keyvalue,
						questionIdXml: questionIdXml,
					}
					)
				})
				/* this.switchArr.forEach((item, index) => {
					item.switchId = index - 3
					item.switchId >= 0 ? item.switchId = item.switchId + 1 : item.switchId //除去switchId = 0
				}) */
				let maps = {
					questionId: item.id,
					questionIdXml: questionIdXml,
					questionName: item.title,
					targetId: item.targetId,
					questionTempleQuestionJumps: JSON.parse(JSON.stringify(this.switchArr))
				}
				/** 
				 * 数据格式转化
				 */
				this.templateList.push(maps);
				this.switchArr = [];
			}).catch((error) => {

			})
		},
		/*
		* tabs点击操作
		*/
		tabsClick(name) {
			/** 
			 * 缓存请求过的数据，再次点击时不再获取
			 */
			if (this.questionList[name - 1].isGet) {
				return false;
			}
			API.followProblems.list({
				pager: 1,
				limit: 1000,
				otype: name == 1 ? "0" : "0" + (name - 1),
				diseaseId: this.selecetDiseId
			}).then((res) => {
				this.questionList[name - 1].list = res.data;
				this.questionList[name - 1].isGet = true;
			}).catch((error) => {

			})
		},
		/*
		*增加模板配置
		*/
		addTemplate(type) {
			let ids;
			//新增和另存为
			if (this.templateId == 'new' || type == 1) {
				ids = '';
			} else {
				ids = this.templateId;
			}
			API.followTemplate.addList({
				id: ids, //不传表示新增 
				diseaseId: (JSON.parse(JSON.stringify(this.templateForm.diseaseId))).join(','),//疾病id      
				name: this.templateForm.name, //模板名称      
				silencetime: this.templateForm.silencetime,//静默时间      
				outrepeattimes: this.templateForm.outrepeattimes,//重复次数      
				person: this.templateForm.person,    //女声传0 男声传1      
				status: 0, //0 正常 1 停用      
				submoulds: this.tagCount.length > 1 ? (JSON.parse(JSON.stringify(this.tagCount))).join(';') : this.tagCount[0] ? this.tagCount[0] : "", //通用库        
				firsttaskid: this.templateForm.firsttaskid,//起始问题编号      
				questionTempleQuestions: this.templateList
			}).then((res) => {
				this.$Message.success("创建成功");
				setTimeout(() => {
					this.$router.push("/followSetting/followTemplate");
				}, 1500);
			}).catch((error) => {

			})
		},
		/*
		*删除一条模板
		*/
		deleteCol(index, id) {
			this.templateList.splice(index, 1);
			/* 更改了id的xml */
			let code = 1000;
			for (let item of this.templateList) {
				item.questionIdXml = code;
				for (let ite of item.questionTempleQuestionJumps) {
					ite.questionIdXml=code;
				}
				code++;
			}
			for (let item of this.stepThirdQuestion) {
				if (item.id == id) {
					item.isClick = 0;
				}
			}
		}
	},
}
</script>

