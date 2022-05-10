
//if (window.Event) {
//	alert(1);
//    window.onbeforeunload = function(event) {
//    	alert(11);
//    	 submitForm(true, false);
//    }
//} else {
//	alert(2);
//    window.onbeforeunload = function() {
//    	alert(22);
//    	 submitForm(true, false);
//    }
//}
function checkWordNum() {
	var jiandaId = $("#jiandaId").val();
	var wordNum = $("#wordNum").val();
	var flagAnswer = true;
	if(parseInt(wordNum) > 0) {
		if(jiandaId != "") {
			var jiandaIdArr = jiandaId.split(",");
			for(var i=0;i<jiandaIdArr.length;i++) {
				var temp = $("#answer" + jiandaIdArr[i]).html();
				if((wordNum != "" && removeAllSpace(temp).length < parseInt(wordNum)) || (wordNum != "" && removeAllSpace(temp) == "")) {
					$("#noSubmitLimitTime").html("简答题最少输入" + wordNum + "个字才能提交！");
					WAY.box.show({'divid':'noSubmitLimitTimeWin'});
					flagAnswer = false;
					break;
				}
			}
		}
	}
	return flagAnswer;
}

function addChoiceByBType(obj) {
	var qid = $(obj).attr("qid");

	var answerPair=[];
	$(".BType_"+qid).each(function () {
		var name = $(this).attr("index");
		var contentStr = "";
		$(this).find(".choice" + qid).each(function(){
			var radio = $(this).find(":radio");
			if(radio.attr("checked")){
				contentStr = radio.val();
				return false;
			}
		});

		var obj={};
		obj.name = parseInt(name);
		obj.content = (contentStr);
		answerPair.push(obj);
	});

	var answerStr=JSON.stringify(answerPair);
	$("#answer" + qid).val(answerStr);
}

//选题(参数:题型、题目id号、题目编号)
function selectAnswer(type,questionId,qNum) {
	setTimeout(function() {
		if(type == 1 || type == 21) {
			var answers = "";
			var name = "answer" + questionId;
			$("input:checkbox[name="+name+"]:checked").each(function() {
				answers += $(this).val();
	    	});
			$("#answers" + questionId).val(answers);
		}
	},200);
}

function checkEvaluationSelectNum(ele) {
	try{
	var wTop = $(ele).parent().hasClass('w-top');
	var name = "answer" + $('#questionId').val();
	var checkedNum = $("input:checkbox[name=" + name + "]:checked").length;
	checkedNum = parseInt(checkedNum);
	var selectNum = $('#selectNum').val() || 0;
	selectNum = parseInt(selectNum);
	if (wTop) {
		if (checkedNum >= selectNum) {
			var index = $(".w-top li").index(ele);
			if ($('.w-buttom li:eq(' + index + ')').find('input:checked').length == 0) {
				alert('最多选' + selectNum + '项');
				return false;
			}
		}
	} else if (checkedNum > selectNum) {
		if ($(ele).find("input:checked").length == 1) {
			$(ele).find("input:checked").attr("checked", false);
			alert('最多选' + selectNum + '项');
			return false;
		} else {
			return true;
		}
	}
	}catch(err){}
	return true;
}

submitAjaxHandle = null ;
// 交卷
function submitForm(tempSave, isback,callback) {
	
	if(tempSave){
		submitAjaxHandle != null && submitAjaxHandle.abort();
	}
	
	var pos = "";
	try{
		pos = getEnc();
	}catch(ex){}
	var examsystem = $("#examsystem").val();
	var qId = $("#questionIds").val();
	var timeOver = $("#timeOver").val();
	var qIdArr =qId && qId.split(",") || [];
	var flag = false;
	var tipStr = "";
	var examsystem=$("#examsystem").val();
	var cpi = $("#cpi").val();
	var openc = $("#openc").val() || '';
	if(typeof(cpi)=="undefined"){
		cpi = 0;
	}
	
	$("#tempSave").val(tempSave);
	if(tempSave == false && isback == false && timeOver == "false") {
//		if(!checkWordNum()) {
//			return;
//		}
		
	  	var submitLimitTime = $("#submitLimitTime").val();
		var limitTime = $("#limitTime").val();
		var temp1 = limitTime * 60 - maxtime;
		var submitLimitTimeTemp = submitLimitTime * 60;
//		if(parseInt(temp1) < parseInt(submitLimitTimeTemp)) {
//			var temp2 =  Math.floor((parseInt(submitLimitTimeTemp) - parseInt(temp1))/60);
//			if(parseInt(temp2) > 0) {
//				$("#noSubmitLimitTime").html("您需要" + temp2 + "分钟后才可交卷");
//				WAY.box.show({'divid':'noSubmitLimitTimeWin'});
//				return;
//			}
//		}
	}
	
	if(tempSave == false && timeOver == "false" && isback == false) {
		for(var i=0;i<qIdArr.length - 1;i++) {
			var id = qIdArr[i];
			var type =$("#"+id).attr("data1");
			if(type == "0") {
				//var answer = $("input:radio[name=answer"+id+"]:checked").val();
				flag = true;
				tipStr = "单选题";
				break;
			} else if(type == "1") {
				//多选
				//var answer = $("#answers" + id).val();
				flag = true;
				tipStr = "多选题";
				break;
				
			} else if(type == "2") {
				//填空
				tipStr = "填空题";
				flag = true;
				break;
			} else if(type == "9") {
				//完型填空
				tipStr = "完型填空题";
				flag = true;
				break;
			}else if(type == "11") {
				tipStr = "连线题";
				flag = true;
				break;
			}else if(type == "12") {
				tipStr = "投票题";
				flag = true;
				break;
			} else if (type == "13") {
				tipStr = "排序题";
				flag = true;
				break;
			} else if (type == "14") {
				tipStr = "完型填空";
				flag = true;
				break;
			} else if (type == "15") {
				tipStr = "阅读理解";
				flag = true;
				break;
			} else if (type == "16") {
				tipStr = "综合题";
				flag = true;
				break;
			} else if (type == "18") {
				tipStr = "口语题";
				flag = true;
				break;
			} else if (type == "19") {
				tipStr = "听力题";
				flag = true;
				break;
			} else if (type == "3") {
				//判断
				flag = true;
				tipStr = "判断题";
				break;
			}else if (type == "20") {
				//判断
				flag = true;
				tipStr = "共用选项题";
				break;
			} else if (type == "21") {
				//判断
				flag = true;
				tipStr = "测评题";
				break;
			} else {
				flag = true;
				tipStr = "简答题";
				break;
			}
		}
	}

	
	if(flag && tempSave == false && timeOver == "false" && isback == false) {
		$("#tipContent").html("您还有未做完的"+tipStr+"，确认提交？");
		WAY.box.show({'divid':'confirmWin'});
	} else if(tempSave == false && timeOver == "false" && isback == false) {
		$("#tipContent").html("确认提交？");
		WAY.box.show({'divid':'confirmWin'});
	} else {
		setStuAnswerOfSomeQues();//对于一些题型 需要提交前设置答案参数
		var param = getParamStr() + "&pos=" + pos + "&version=1";
		//临时保存或时间到系统自动提交试卷
		var ajax_url = "/exam/test/reVersionSubmitTestNew"+param; //表单目标     
		var ajax_type = "post"; //提交方法 
		var ajax_data = $("#submitTest").serialize(); //表单数据

        submitAjaxHandle = $.ajax({
			type : ajax_type,
			url : ajax_url,
			data :ajax_data,
			dataType: "json",
			success : function(result){
				var status = result.status;
				var msg = result.msg;
				
				if(status == "error"){
					alert(msg);
					submitFlag = true;
					return ;
				}
				
				if(status == "submitted" || status == "forceSubmitted"){
					removeTimeOverSubmitTimers();
					closeMonitor();
					//alert("考试已经提交，正在跳转...");
					WAY.box.show({'divid':'submitedWin'});
					setTimeout("goExamList()",1200);
					return;
				}
				
				if(tempSave){
					 answerRecordLog && answerRecordLog(result.monitorparam);
				}else{
					finalSubmitExamLog({'submitStyle' : 0});
				}
				
				var courseId = $("#courseId").val();
				var classId = $("#classId").val();
				
				if(isback == true) {
					closeMonitor();
					goExamList();
				} else if(timeOver == "true"){
					removeTimeOverSubmitTimers();
					closeMonitor();
					var consumeMinutes = result.consumeMinutes || 0;
					if(consumeMinutes > 0){
						$('.consumeMinutes').html(consumeMinutes);
					}
					WAY.box.show({'divid':'timeOverWin'});
					setTimeout(function(){
						goExamList();
					},3000);
				}else {
					//alert(data);
					setTimeout(function(){
						callback && callback(result.data);//relationAnswerLastUpdateTime
					},10);
				}
	
			},
			error: function(result){
				//document.write(result.responseText);
			},
			complete : function(){
				submitAjaxHandle = null;
			}
		});
		
	}
	 
}

var timersTip;
//提交
function confirmSubTest() {
	//timers2 = clearInterval(timers2);
	var pos = "";
	try{
		pos = getEnc();
	}catch(ex){}
	var param=getParamStr();//带此参数方便查询操作日志
	param = param + "&pos=" + pos + "&version=1";
	timers = clearInterval(timers);
	$(".scrolllist").hide();
	timersTip = setInterval("CountDownTip()",1000);
	WAY.box.show({'divid':'handleWin'});
	var ajax_url = "/exam/test/reVersionSubmitTestNew"+param; //表单目标     
	var ajax_type = "post"; //提交方法 
	var ajax_data = $("#submitTest").serialize(); //表单数据
	$.ajax({
		type : ajax_type,
		url : ajax_url,
		data :ajax_data,
		dataType: "json",
		success : function(result){
			var status = result.status;
			var msg = result.msg;
			if(status == "error"){
				timersTip && clearInterval(timersTip);
				alert(msg);
				window.location.reload();
			}
			if(status == "submitted" || status == "forceSubmitted"){
				closeMonitor();
				timersTip && clearInterval(timersTip);
				//alert("考试已经提交，正在跳转...");
				WAY.box.show({'divid':'submitedWin'});
				setTimeout("goExamList()",1200);
			}
			if (status == "success") {
				finalSubmitExamLog({'submitStyle' : 0});
				closeMonitor();
				var ut = "s";
				WAY.box.show({'divid':'submitSuccessTipWin'});
				setTimeout("goExamList()",1500);
			}
		},
		error: function(){
			timersTip && clearInterval(timersTip);
			alert("提交考试异常啦，稍后再试.");
			window.location.reload();
		}
	});
}

function goExamList() {
	var qbanksystem =  $('#qbanksystem').val();
	var qbankbackurl =  $('#qbankbackurl').val();
	if(qbanksystem == 1 && qbankbackurl != ''){
		qbankbackurl = decodeURIComponent(qbankbackurl);
		location.href = qbankbackurl;
		return;
	}
	
	var courseId = $("#courseId").val();
	var classId = $("#classId").val();
	var cpi = $("#cpi").val();
	var openc = $("#openc").val() || '';
	if(typeof(cpi)=="undefined"){
		cpi = 0;
	}
	var examsystem=$("#examsystem").val();
	location.href = "/exam/test?classId="+classId+"&courseId=" + courseId +"&cpi=" +cpi+ "&ut=s"  + 
	"&examsystem=" + examsystem + "&openc=" + openc; 
}

function timeOverSubmitTest() {
	if(!window.OverTimeSubmitTimers){
		window.OverTimeSubmitTimers = [];
	}
	var overTimeSubmitTimers =  window.OverTimeSubmitTimers;
	for (var i = 0; i < 3; i++) {
	    var overTimer = setTimeout(function() {
			submitForm(false, false);
		}, i * 5000);
	    overTimeSubmitTimers.push(overTimer);
	}
}

function removeTimeOverSubmitTimers(){
	var overTimeSubmitTimers = window.OverTimeSubmitTimers;
	if(!overTimeSubmitTimers || overTimeSubmitTimers.length == 0){
		return ;
	}
	for(var i = 0 ; i < overTimeSubmitTimers.length; i++){
		var overTimeSubmitTimer = overTimeSubmitTimers[i];
		if(overTimeSubmitTimer){
			clearTimeout(overTimeSubmitTimer);
		}
	}
}

function CountDownTip(){  
	if(maxSecond == 0){
		timersTip && clearInterval(timersTip);
		WAY.box.hide();
		alert('考试提交超时，如果页面未跳转，  请重新提交考试！');
		window.location.reload();
	}
    if(maxSecond>0){
		 $("#subTip").html(maxSecond);
		 --maxSecond;
    } 
    /* else{
	 	var courseId = $("#courseId").val();
		var classId = $("#classId").val();
       location.href = "/exam/test?classId="+classId+"&courseId=" + courseId;
    }  
    */
}


function getParamStr(){
    var testPaperId=$("#testPaperId").val();
    var testUserRelationId=$("#testUserRelationId").val();
    var courseId=$("#courseId").val();
    var classId=$("#classId").val();
    var tempSave=$("#tempSave").val();
    var cpi=$("#cpi").val();
    if(typeof(cpi)=="undefined"){
		cpi = 0;
	}
    var param="?classId="
    	+ classId
    	+ "&courseId="
    	+ courseId
    	+ "&testPaperId="
    	+ testPaperId
    	+ "&testUserRelationId="
    	+ testUserRelationId
    	+ "&cpi="
    	+ cpi
    	+ "&tempSave="
    	+ tempSave;
    return param;
}


function removeAllSpace(str) {
	return str.replace(/<\s?img[^>]*>/gi, "图片").replace(/<[^>]+>/g,"").replace(/&nbsp;/ig,"").replace(/\s+/g, "");
//		return str.replace(/<[^>]+>/g,"").replace(/&nbsp;/ig,"").replace(/\s+/g, "");
}





function scroller(type,qNum) {
	var id = "position" + type + qNum;
	var scroll_offset = $("#" + id).offset();  //得到pos这个div层的offset，包含两个值，top和left
	$("body,html").animate({
		scrollTop:scroll_offset.top  //让body的scrollTop等于pos的top，就实现了滚动
	},0);
}
//填空题
function selectAnswerBlank(type,questionId,qNum,blankNum) {
	setTimeout(function() {
		var isfinish = true;
		for(var i=1;i<=blankNum;i++) {
			var answerName = "answer";
			var divTmp = $("#answerEditor" + questionId + i).parent();
			if(!$(divTmp).is(":hidden")) {
				answerName = "answerEditor";
			}
			var content = $("#" + answerName + questionId + i).val();
			if(typeof(content) == "undefined" || removeAllSpace(content).length == 0) {
				isfinish = false;
				break;
			}
		}
		if(isfinish) {
			$("#span" + type + qNum).attr("class","dasure danull");
		} else {
			$("#span" + type + qNum).attr("class","dasure");
		}
	},200);
	
}
//简答题
function selectAnswerShort(type,questionId,qNum) {
	setTimeout(function() {
		var content = $("#answer" + questionId).val();
		if(typeof(content) != "undefined" && removeAllSpace(content).length != 0) {
			$("#span" + type + qNum).attr("class","dasure danull");
		} else {
			$("#span" + type + qNum).attr("class","dasure");
		}
	},200);
}


function setStuAnswerOfSomeQues(){
	
	var nowQuestionId=$("#questionId").val();
	if(!nowQuestionId){
		return;
	}
	var nowTypeQuestionId="type"+nowQuestionId;
	var questionType=$("input[name='"+nowTypeQuestionId+"']").val();
  
  // 避免自动提交时简答题答案丢失
	 if (questionType == 4 || questionType == 5 || questionType == 6 || questionType == 7 || questionType == 8 || questionType ==17 || questionType == 18) {
			var me = UE.getEditor('answer' + nowQuestionId);
			me && me.sync();
	 }else if (questionType == 2 || questionType == 9 || questionType == 10) {
			var blankStr = "answerEditor" + nowQuestionId;
			var blankInputs = $("textarea[name^='" + blankStr + "']");
			blankInputs.length > 0 && blankInputs.each(function () {
				var blankEditorId = $(this).attr('id');
				if(blankEditorId){
				    var me = UE.getEditor(blankEditorId);
				    me && me.sync();
				}
			});
    }
	
	if(questionType==11){
		var answerPair=[];
		$(".thirdUlList select").each(function(index){
			var checked=$(this).val();
			var obj={};
			obj.name=(index+1);
			obj.content=(checked);
			answerPair.push(obj);
		});
		var answerStr=JSON.stringify(answerPair);
		$("input[name='answer"+nowQuestionId+"']").val(answerStr);
	}else if(questionType==13){
		var answerStr="";
		$(".sortQuesSelect select").each(function(index){
			var checked=$(this).val();
			answerStr=answerStr+checked;
		});
		$("input[name='answer"+nowQuestionId+"']").val(answerStr);
		
	}else if(questionType==14){//新完型填空
		var answerObj={};
		$(".Cy_ulTop li").each(function(index){
			var itemId=$(this).find("input[name='itemId']").val();
			var checked=$(this).find("input[type='radio']:checked").val();
			if(checked==undefined){
				checked="";
			}
			var info={};
			info.answer=checked;
			answerObj[itemId]=info;
		});
		var answer=[];
		answer.push(answerObj);
		var answerStr=JSON.stringify(answer);
		$("input[name='answer"+nowQuestionId+"']").val(answerStr);
	   } else if (questionType == 15 || questionType == 16 || questionType == 19) {// 新阅读理解、综合题
		var answerObj={};
		$("input[name='readCompreHension-childType']").each(function(index){
			var type=$(this).val();
			var itemId=$(this).next().val();
			var itemAnswer="";
			switch(parseInt(type)){
				case 0:
				case 3:{
					itemAnswer=$("input[type='radio'][name='answer"+itemId+"']:checked").val();
					if(type==3){
					  itemAnswer=itemAnswer?(itemAnswer=="true"?true:false):itemAnswer;
					}
					break;
				}
				case 1:{
					$("input[type='checkbox'][name='answer"+itemId+"']:checked").each(function() {
						itemAnswer +=$(this).val();
						var randomOptions = $("#randomOptions").val();
						itemAnswer = randomOptions ? sortMultiAnswer(itemAnswer) : itemAnswer;
					});
					break;
				}
				case 2:{
					  var answerItem=[];
					  var blankNum=$("input[name='"+itemId+"blankNum']").val();
					for(var i=1;i<=blankNum;i++){
						// var blankInputId="answer"+itemId;
						// var answerEditorId="answerEditor"+itemId;
						// blankInputId=blankInputId+i;
						// answerEditorId=answerEditorId+i;
						// var blankInput=$("input[name='"+blankInputId+"']");
						// var  answerItemStr=blankInput.val();
						// var answerEditorStr=UE.getEditor(answerEditorId).getContent();
						// if(blankInput.parent().is(":hidden")){
						//  answerItemStr=answerEditorStr;
						// }
                        var answerEditorId="answerEditor"+itemId;
                        answerEditorId=answerEditorId+i;
                        var answerItemStr=UE.getEditor(answerEditorId).getContent();
						var item={};
						item.content=answerItemStr;
						item.name=i.toString();
						answerItem.push(item);
					}
					itemAnswer=answerItem;
					break;
				}
				case 4:{
					var answerEditorId="answer"+itemId;
					var answerEditorStr=UE.getEditor(answerEditorId).getContent();
					itemAnswer=answerEditorStr;
					break;
				}
				default: { }
			}
			
			var info={};
			info.type=parseInt(type);
			
			info.answer=(itemAnswer!=undefined?itemAnswer:"");
			answerObj[itemId]=info;
			//console.log(type+"  "+itemId+"  "+itemAnswer);
		});
		var answer=[];
		answer.push(answerObj);
		var answerStr=JSON.stringify(answer);
		$("input[name='answer"+nowQuestionId+"']").val(answerStr);
		//console.log(answerStr);
	} else if (questionType == 17) {
		var answer = [];
		var language=$("#languageSelect").val();
		var richcode=editor.getContent();
		var code=editor.getPlainTxt(); code=UE.utils.html(code);
		var item={};
		item.language=parseInt(language);
		item.answer=richcode;
		item.answerTxt=code;
		answer[0]=item;
		var answerStr = JSON.stringify(answer);
		$("input[name='answer" + nowQuestionId + "']").val(answerStr);
	
		$("#procedural-mask").css("display", "block");
		setTimeout(function() {
			$("#procedural-mask").css("display", "none");
		}, 10000);
		
	}else if(questionType == 1){
		var randomOptions = $("#randomOptions").val();
		var multipleChoiceInput=$("input[name='answers" + nowQuestionId + "']");
		var mulChoice=multipleChoiceInput.val();
		mulChoice = randomOptions ? sortMultiAnswer(mulChoice) : mulChoice;
		multipleChoiceInput.val(mulChoice);
	}

}

function sortMultiAnswer(answer) {
	if ( !answer || answer.trim().length == 0) {
		return "";
	}
	var answerArray = answer.trim().split('');
	var sortedAnswerArray = answerArray.sort();
	var sortedAnswer = sortedAnswerArray.join('');
	return sortedAnswer;
}


//首次进入考试日志
function entryExamLog(data){
	var snapshotMonitor = $('#snapshotMonitor').val();
	if(snapshotMonitor != 1){
		return;
	}
	var eventType = 0;
	pushExamMonitorLog(eventType,data);
}

//重新进入考试日志
function rentryExamLog(data){
	var snapshotMonitor = $('#snapshotMonitor').val();
	if(snapshotMonitor != 1){
		return;
	}
	var eventType = 1;
	pushExamMonitorLog(eventType,data);
}

//最终提交考试日志
function finalSubmitExamLog(data){
	var snapshotMonitor = $('#snapshotMonitor').val();
	if(snapshotMonitor != 1){
		return;
	}
	var eventType = 2;
	pushExamMonitorLog(eventType,data);
}


//提交答案日志
function answerRecordLog(answerData){
	var snapshotMonitor = $('#snapshotMonitor').val();
	if(snapshotMonitor != 1){
		return;
	}
	if(!answerData){
		return;
	}
	var eventType = 3;
	pushExamMonitorLog(eventType,answerData);
}

//切屏日志
function switchScreenLog(data){
	var switchScreenControl = $('#switchScreenControl').val();
	if(switchScreenControl != 1){
		return;
	}
	if(!data){
		return;
	}
	var status = data.status;
	var eventType = 9;
    if(status == 1){
    	eventType = 10;
    }
	pushExamMonitorLog(eventType,data);
}

//监控抓拍日志
function snapshotMonitorLog(data){
	var snapshotMonitor = $('#snapshotMonitor').val();
	if(snapshotMonitor != 1){
		return;
	}
	  if(!data){
			return;
	  }
	  var funconfig = JSON.parse(data.funconfig || data.funConfig);
	  var answerId = $('#testUserRelationId').val();
	  var classId = $('#classId').val();
	  if(funconfig.answerId != answerId || funconfig.classId != classId){
		  return;
	  }
	  var similarity = data.similarity;
	  var status = true;
	  if(similarity < 50){
		  status = false;
	  }
	  data.status = status;
	  var eventType = 5;
	  pushExamMonitorLog(eventType,data);
}


function pushExamMonitorLog(eventType,data) {
	try{
		var url = '/keeper/api/receiveExamLogs';
		var currentFaceId=data.currentFaceId;
		if(eventType==0 && (typeof(currentFaceId) == "undefined" || currentFaceId=="")){
			var _version = data.version;
			if (typeof (_version) != "undefined" && _version != -1) {
				url = '/keeper/api/receiveExamLogs?currentFaceId=false&eventType=' + eventType;
			}
		}
		var eventTime = new Date().getTime();
		var ip = "";
		if (eventType == 1) {
			eventTime = data.rentryExamTime;
		} else if (eventType == 2) {
			eventTime = data.finalSubmitTime;
		} else if (eventType == 3) {
			eventTime = data.submitTime;
		}

		//data.device = 1;

		var courseId = $('#courseId').val();
		var examRelationId = $('#testPaperId').val();
		var answerId = $('#testUserRelationId').val();
		var clazzId = $('#classId').val();
		var personId = $('#cpi').val();
		var log = {
				"courseId":courseId,
				"clazzId": clazzId,
				"personId":personId,
				"examRelationId":examRelationId,
				"answerId":answerId,
				"eventType":eventType,
				"ip":ip,
				"data":data
		};
	    var monitorEnc = $('#monitorEnc').val();
		$.ajax({
			type : 'post',
			dataType : 'json',
			url : url,
			data : {"log":JSON.stringify(log), "enc":monitorEnc},
			success : function(data) {
			}
		});
	}catch(err){}
}

//关闭考试监控项
function closeMonitor(){
	closeExamClientFaceMonitor();
	closeExamClientScreenCutting();
}

//调起客户端切屏协议
function openExamClientScreenCutting() {
	var pcclientSwitchout = $('#pcclientSwitchout').val();
	if (pcclientSwitchout == 1 && window.cef && typeof (window.cef.OpenScreenCutting) == 'function') {
		var switchScreenControl = $('#switchScreenControl').val();
		if (switchScreenControl == 1) {
			window.CLIENT_WEB_LIFECYCLE = function(data) {
				switchScreenLog(data);
			};
		}else{
			window.CLIENT_WEB_LIFECYCLE = function(data) {	};
		}
		var paramObj = {"is_open" : 1};
		window.cef.OpenScreenCutting(JSON.stringify(paramObj));
	}
}
//关闭客户端切屏协议
function closeExamClientScreenCutting() {
	var pcclientSwitchout = $('#pcclientSwitchout').val();
	if (pcclientSwitchout == 1 && window.cef && typeof (window.cef.OpenScreenCutting) == 'function') {
		var paramObj = {"is_open":0};
		window.cef.OpenScreenCutting(JSON.stringify(paramObj));
	}
}

//调起人脸抓拍协议
function openExamClientFaceMonitor(monitorOp, monitorStatus, funconfig) {
	var snapshotMonitor = $('#snapshotMonitor').val();
	if (snapshotMonitor == 1 && window.cef && typeof (window.cef.OpenFaceMonitor) == 'function') {
		window.CLIENT_FACE_COLLECTION = function(data){
			snapshotMonitorLog(data);
		};
		if (monitorOp > 0) {
			var paramObj = {"enable" : "1","internalTime" : monitorStatus,"funconfig" : funconfig};
			window.cef.OpenFaceMonitor && window.cef.OpenFaceMonitor(JSON.stringify(paramObj));
		} else if (monitorOp == 0) {
			closeExamClientFaceMonitor();
		}
	}
}
//关闭人脸抓拍协议
function closeExamClientFaceMonitor(){
	var snapshotMonitor = $('#snapshotMonitor').val();
	if(snapshotMonitor == 1 && window.cef && typeof (window.cef.OpenFaceMonitor) == 'function') {
		var paramObj = {"enable" : "0","internalTime" : "-1","funconfig" : ""};
		window.cef.OpenFaceMonitor && window.cef.OpenFaceMonitor(JSON.stringify(paramObj));
	}
}



function checkRemainTime(status) {
	
	if (status == 'hidden') {
		window.Leave_Exam_Page = new Date().getTime();
		window.Leave_SingleQuesLimitTime = SingleQuesLimitTime || -1;
	} else if (status == 'visible') {
		window.Back_Exam_Page = new Date().getTime();
	}
	var leaveTime = window.Leave_Exam_Page || 0;
	var backTime = window.Back_Exam_Page || 0;
	var threshold = 1 * 60 * 1000;
	if (leaveTime > 0 && backTime > 0 && (backTime - leaveTime) >= threshold) {
		checkSingleQuesLimitTimeRemainTime();
		fireCheckRemainTime();
	}

	function fireCheckRemainTime() {
		var formParams = $("#submitTest").serialize();
		$.ajax({
			type: 'post',
			url: '/mooc2/exam/check-remaintime',
			data: formParams,
			dataType: 'json',
			success: function (result) {
				delete window.Leave_Exam_Page;
				delete window.Back_Exam_Page;
				delete window.Leave_SingleQuesLimitTime;
				var status = result.status;
				var seconds = result.data;
				if (!status || !seconds || seconds < 1) {
					return;
				}
				clearInterval(timers);
				maxtime = seconds;
				timers = setInterval("CountDown()", 1000);
			}
		});
	}
	
}

function validateAudioPlayTimes(frameElement) {
	var frameElementObj = $(frameElement);
	var mid = frameElementObj.attr('mid') || '';
	var objectid = frameElementObj.attr('data') || '';
	var playtimeslimit = frameElementObj.attr('playtimeslimit') || 0;
	if(mid == '' || objectid == '' || playtimeslimit  <= 0){
		return;
	}
	var quesId = $(frameElement).parents('.singleQuesId').attr('data') || '';
	var ajax_url = '/exam/test/audio-playtimes?qid=' + quesId  + '&mid=' + mid + '&objectid=' + objectid + '&times=' + playtimeslimit ; 
	var ajax_type = "post"; 
	var ajax_data = $("#submitTest").serialize(); 
    submitAjaxHandle = $.ajax({
		type : ajax_type,
		url : ajax_url,
		data :ajax_data,
		dataType: "json",
		success : function(result){
			var status = result.status;
			if(status == 0){
				frameElement.contentWindow.stopAudioPlay();
				$('.audioLimitTimesTip span').text(playtimeslimit);
				WAY.box.show({'divid': 'audioLimitTimesWin'});
				return ;
			}
		}
	});
}

function replaceAttachPreviewPath() {
	$('a[href^="/ueditorupload/read"]').each(function() {
		var href = $(this).attr('href') || '';
		href = href.replace('/ueditorupload/read', '/examattach/read');
		$(this).attr('href', href);
	});
	window.ATTACH__NO_DOWNLOAD_PATH = '/examattach/read';
}

$(document).ready(function() {
	var allowDownloadAttachment  =	$("#allowDownloadAttachment").val();
	if (!(typeof allowDownloadAttachment != "undefined" && allowDownloadAttachment == "1")) {
		replaceAttachPreviewPath();
	}
	removeImageTitle();
});


function removeImageTitle(){
	$('.TiMu img').each(function(){
		$(this).removeAttr('title');
	});
}


function callback_exam(obj) {
	var winId = "multiTerminalWin";
	if($('#' + winId).is(':visible')){
		return;
	}
	var confirmFunction = function() {
		submitForm(true, false, function() {
			var url = window.location.href;
			if (url && url.indexOf('tag=1') != -1) {
				url = url.replace('tag=1', 'tag=0');
				window.location.href = url;
			}else{
				window.location.reload(true);
			}
		});
	};
	var cancelFunction = function() {
		submitForm(true, true);
		WAY.box.hide();$('#multiTerminalWin').css('display','none');
	};
	
	var confirmBtn = $('#' + winId).find('.confirm');
	var cancelBtn = $('#' + winId).find('.cancel');
	confirmBtn.off('click');
	cancelBtn.off('click');
	confirmBtn.on('click',confirmFunction);
	cancelBtn.on('click',cancelFunction);
	var message = obj.mes;
	$('#' + winId).find('.tipContent').html(message);
	WAY.box.show({
		'divid' : winId
	});
}


function answerDirectSubmit(){
	submitForm(false, false);
}

var SingleQuesLimitTime;
function checkStartSingleQuesLimitTimeTimer() {
	var limitTimeType = $('#limitTimeType').val() || 0;
	if(limitTimeType == 0){
		return;
	}
	SingleQuesLimitTime =  loadSingleQuesLimitTime();
	if(SingleQuesLimitTime < 0){
		SingleQuesLimitTime = $('#singleQuesLimitTime').val();
	}
	if (SingleQuesLimitTime >= 0) {
		var clockTime = secondsToClockTime();
		$(".singleQuesLimitTimeClock").html(clockTime);
		singleTimerHandle = setInterval("singleQuesLimitTimeTimer()", 1000);
	}
}

function secondsToClockTime(){
	var minutes = '00';
	var seconds = '00';
	var clockTime = minutes + ':' + seconds ;
	if (SingleQuesLimitTime > 0) {
	    minutes = Math.floor(SingleQuesLimitTime / 60);
		if (minutes < 10) {
			minutes = "0" + minutes;
		}
		seconds = Math.floor(SingleQuesLimitTime % 60);
		if (seconds < 10) {
			seconds = "0" + seconds;
		}
		clockTime = minutes + ':' + seconds ;
	}
	return clockTime;
}

function singleQuesLimitTimeTimer() {
	var clockTime = secondsToClockTime();
	$(".singleQuesLimitTimeClock").html(clockTime);
	$("#singleQuesLimitTime").val(SingleQuesLimitTime);
	storeSingleQuesLimitTime(SingleQuesLimitTime);
	if (SingleQuesLimitTime > 0) {
		--SingleQuesLimitTime;
	} else {
		clearInterval(singleTimerHandle);
		WAY.box.show({'divid' : 'singleQuesLimitTimeWin'});
	}
}

function storeSingleQuesLimitTime(seconds){
	if(!window.sessionStorage){
		return;
	}
	if(sessionStorage.length > 1){
		sessionStorage.clear();
	}
	var receiveTime = $('#receiveTime').val() || 0;
	var key =  'singleQuesLimitTime_' + receiveTime + "_" + $('#testUserRelationId').val() + "_" + $('#classId').val() + "_" + $('#questionId').val();
	sessionStorage.setItem(key, seconds);
}

function loadSingleQuesLimitTime(){
	if(!window.sessionStorage){
		return -1;
	}
	if($('#forbidAnsweredAgain').val() == 1){
		return -1;
	}
	var receiveTime = $('#receiveTime').val() || 0;
	var key =  'singleQuesLimitTime_' + receiveTime + "_" + $('#testUserRelationId').val() + "_" + $('#classId').val() + "_" + $('#questionId').val();
	var seconds = sessionStorage.getItem(key);
	if(seconds != null && $.isNumeric(seconds)){
		return parseInt(seconds);
	}
	return -1;
}

function singleQuesLimitTimeConfirm(submit){
	if(submit && submit == 1){
		$("#timeOver").val(true);
		submitForm(false,false);
		return;
	}
	getTheNextQuestion(1);
}


function checkSingleQuesLimitTimeRemainTime(){
	var limitTimeType = $('#limitTimeType').val() || 0;
	if(limitTimeType == 0){
		return;
	}
	
	var leaveTime = window.Leave_Exam_Page || -1;
	var backTime = window.Back_Exam_Page || -1 ;
	if (leaveTime <=0 || backTime <= 0) {
		return;
	}
	
	var singleQuesLimitTime = window.Leave_SingleQuesLimitTime || -1;
	if (singleQuesLimitTime < 0) {
		return;
	}
	
	var diffMillSeconds = parseInt(backTime) - parseInt(leaveTime);
	var useSeconds = Math.ceil((diffMillSeconds / 1000).toFixed(3));
	if(useSeconds <= 0){
		return
	}
	
	var remainSeconds = parseInt(singleQuesLimitTime) - parseInt(useSeconds);
	if(remainSeconds <= 0){
		remainSeconds  = 1;
	}
	clearInterval(singleTimerHandle);
	SingleQuesLimitTime = remainSeconds;
	singleTimerHandle = setInterval("singleQuesLimitTimeTimer()", 1000);
}
