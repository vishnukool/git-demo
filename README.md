
It added to REAME.
VISHNU IS KOOL


<jsp:directive.page import="com.btsl.common.util.Constants" />

<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN">


<%@ taglib uri="/struts-tags" prefix="s"%>
<%@page contentType="text/html;charset=UTF-8" import="java.util.*"%>
<s:head theme="qajax" />
<script language="javascript">
function checkSpace(e){
      if(e.keyCode==32){   
             return false;
      }
}
//DEF507 start
window.onload = function() {
	var expLabel = $("#explabel").text();
	var exp = $("#exp").text();
	var asterisk = "*";
	var redasterisk = asterisk.fontcolor("red");
	expLabel = expLabel.concat(redasterisk+":").bold();
	exp = exp.concat(redasterisk+":").bold();
	$("#explabel").html(expLabel);
	$("#exp").html(exp);
	hidepicker();
} 
function hidepicker(){
	var idexp=document.subsRegistrationServiceBean.isIdExpires.checked;
	if(idexp){
		  $("#idExpiryDate").show();
		  $("#exp").show();
	}
	else{
		  $("#idExpiryDate").hide();
		  $("#exp").hide();
	}	
}
//DEF507 end
</script>
<html>
	<body>
		<%--<s:text name="%{getText('form.fields.mandatory')}" />
		--%>

		<s:bean name="java.util.HashMap" id="qTableLayout">
			<s:param name="tablecolspan" value="%{4}" />
		</s:bean>
         <%-- DEF1289 start --%>
		<s:form name="subsRegistrationServiceBean" validate="true" id="subsRegistrationServiceBean"
			namespace="/party" theme="qxhtml" enctype="multipart/form-data">
			<%-- DEF1289 end --%>
			<%--  added for 2.0.0.12 merge  --%>
			<s:include value="/mjsp/common/includeCSRFTokenGenerator.jsp"></s:include>
			<%-- ends here --%>

			<%--<s:select name="partyData.userNamePrefix" headerKey=""
				required="true" headerValue="Select"
				key="subs.approval.label.nameprefix" list="namePrefixList"
				listKey="enumId" listValue="description" value="select" />	--%>
				
			<s:component cssClass="tabhead" template="/components/textcell.ftl"
				value="%{getText('subs.approval.information')}">
				<s:param name="inputcolspan" value="%{4}" />
			</s:component>

			<%--<s:textfield name="userNamePrefix" key="subs.approval.label.nameprefix" maxlength="15" />
					
			--%>
			
			<!-- Start  Added for Aadhaar Integration -->
		<s:if test="adharIdRequired"> 
			  <OBJECT classid='clsid:CAFEEFAC-0016-0000-0000-ABCDEFFEDCBA' WIDTH = 0 HEIGHT = 0 NAME = 'uidfrm' ID = 'uidfrm' ALIGN = middle VSPACE = 0 HSPACE = 0>
		        <PARAM NAME = CODE VALUE = 'com.integra.uid.XmlApplet.class' >
		        <PARAM NAME = CODEBASE VALUE = '<%=request.getContextPath()+"/mjsp/dep-lib/"%>' >
		        <PARAM NAME = ARCHIVE VALUE = 'uidApplet.jar,bcprov-jdk16-140.jar,commons-codec-1.4.jar,plugin.jar,json.jar' >
		        <PARAM NAME = NAME VALUE = 'UID-Payload-Generator' >
		        <PARAM NAME='type' VALUE='application/x-java-applet;version=1.6'>
		        <PARAM NAME='scriptable' VALUE='true'>        
		        <PARAM name='uidPublicKeyPath' value='<%=request.getScheme()+"://"+request.getServerName()+":"+request.getServerPort()+request.getContextPath()+"/mjsp/dep-lib/uidai_auth_prod.cer"%>'>
		        <PARAM name='xmlNameSpace' value='http://www.uidai.gov.in/authentication/uid-auth-request/1.0' />
		        <PARAM name='fileKey' value='<%=request.getScheme()+"://"+request.getServerName()+":"+request.getServerPort()+request.getContextPath()+"/mjsp/dep-lib/public-may2012.p12"%>'>
		      </OBJECT>			
				
				<input type="hidden" id="auth_xml" name="auth_xml" value=""/>
				<s:hidden id="isSigned" name="isSigned" value="true"/>
				<s:hidden id="aadharNumber" name="aadharNumber" value="true"/>  
				<s:hidden name="aadharUidLen" id="aadharUidLen" />			
			 <tr>
					<td class="tabtextbold">
						<s:text name="Subs.registration.label.UID"  />
						
					</td>
					<td class="tabcol">
						<s:textfield theme="simple" maxlength="%{aadharUidLen}"  
							name="uID"  id="uID"
							required="true" />
					</td>
					<td class="tabcenter" colspan="1" theme="bsimple">
						<s:submit key="button.authenticate" cssClass="btn1" theme="bsimple"
							id="checkUIDAvail" onclick="validateBiometricInformation(); return false;" />
					</td>
					<td class="tabcenter" colspan="1">
						<span id="availUidAadhar" class="tabtextbold" />&nbsp; 
					</td>
				</tr>		
				
			</s:if>
			<!-- End  Added for Aadhaar Integration -->
            
			<s:select name="userNamePrefix" headerKey=""  disabled="%{isDisable}"
				headerValue="Select" required="!treeset.contains('userNamePrefix')"
				 key="subs.approval.label.nameprefix"
				list="namePrefixList" listKey="enumId" listValue="description" />

			<s:textfield name="userName"  key="Subs.registration.label.UserName" maxlength="80" required="!treeset.contains('userName')" disabled="%{isDisable}" />
				<%-- modified by gaurav  --%>
			<s:textfield name="middleName" key="Subs.registration.label.MiddleName" maxlength="15" required="!treeset.contains('middleName')"  disabled="%{isDisable}"/> 
			
			<s:textfield name="lastName" key="systemparty.label.lastName" maxlength="80" required="!treeset.contains('lastName')" disabled="%{isDisable}" />
              <!-- Added By Dhananjay samal -->
			
			<s:select name="nationality" headerKey="" required="!treeset.contains('nationality')"
				headerValue="%{getText('select.label')}" disabled="%{isDisable}"
				key="channeluser.label.nationality"
				list="nationalTypeIdList" listKey="countryIso"
				listValue="description" />
		<s:label name=""></s:label>
		<s:label name=""></s:label>
				
			<s:if test='isAvailButtonRequired.equals("Y")'>
				<tr>
					<td class="tabtextbold">
						<s:text name="Subs.registration.label.Msisdn" />
						<font color="red">*</font>:
					</td>
					<td class="tabcol">
						<s:textfield theme="simple" maxlength="%{checkMsisdnLen}" disabled="%{isDisable}"
							name="msisdn" label="Msisdn" key="msisdn" id="msisdn"
							required="!treeset.contains('msisdn')" />
					</td>
					<td class="tabcenter" colspan="1" theme="bsimple">
						<s:submit key="button.check" cssClass="btn1" theme="bsimple" disabled="%{isDisable}"
							id="checkMSISDNAvail" onclick="checkMsisdn(); return false;" />
					</td>
					<td class="tabcenter" colspan="1">
						<span id="availMSISDN" class="tabtextbold" />&nbsp; 
					</td>
				</tr>
				
				<tr>
				<s:if test='isIdRequireRequired.equals("Y")'>
					<td class="tabtextbold">
						<s:text name="subs.approval.label.extcode" />
						<font color="red">*</font>:
					</td>
					<td class="tabcol">
						<s:textfield theme="simple" maxlength="%{checkExtCodeLen}" disabled="%{isDisable}"
							name="externalCode" label="External Code" key="externalCode"
						required="!treeset.contains('externalCode')"	id="externalCode"/>
					</td>
					<td class="tabcenter" colspan="1">
						<s:submit key="button.check" cssClass="btn1" theme="bsimple" disabled="%{isDisable}"
							id="checkExtCodeAvail" onclick="checkExtCode(); return false;" />
					</td>
					<td class="tabcenter" colspan="1">
						<span id="availExtCode" class="tabtextbold" />&nbsp; 
					</td>
					</s:if>
				<s:else>
				<td class="tabtextbold">
						<s:text name="subs.approval.label.extcode" />
					</td>
					<td class="tabcol">
						<s:textfield theme="simple" maxlength="%{checkExtCodeLen}" disabled="%{isDisable}"
							name="externalCode" label="External Code" key="externalCode"
							id="externalCode"/>
					</td>
					<td class="tabcenter" colspan="1">
						<s:submit key="button.check" cssClass="btn1" theme="bsimple" disabled="%{isDisable}"
							id="checkExtCodeAvail" onclick="checkExtCode(); return false;" />
					</td>
					<td class="tabcenter" colspan="1">
						<span id="availExtCode" class="tabtextbold" />&nbsp; 
					</td>
				</s:else>
				</tr>
				
			</s:if>
			<s:else>
				<%-- modified for 2.0.0.12 merge 
	<s:textfield name="msisdn" key="Subs.registration.label.Msisdn" id="msisdn"--%>
				<s:textfield name="msisdn" key="subs.approval.label.msisdn" disabled="%{isDisable}"
					maxlength="%{checkMsisdnLen}" required="!treeset.contains('msisdn')" />
					<s:if test='isIdRequireRequired.equals("Y")'>
				  <s:textfield name="externalCode" key="subs.approval.label.extcode" disabled="%{isDisable}"
					id="externalCode" maxlength="%{checkExtCodeLen}" required="!treeset.contains('externalCode')" />
				</s:if>	
				   <s:else>
				   <s:textfield name="externalCode" key="subs.approval.label.extcode" disabled="%{isDisable}"
					required="!treeset.contains('externalCode')" id="externalCode" maxlength="%{checkExtCodeLen}"  />
				   </s:else>
				
			</s:else>
			<s:textfield name="formno" key="Subs.registration.label.FormNo" required="!treeset.contains('_formno')"
				maxlength="16" />

			<s:datetimepicker key="subs.approval.label.dob"
				displayFormat="dd/MM/yyyy" value=""   name="inputDob" required="!treeset.contains('inputDob')">
				<s:param name="labelcolspan" value="%{1}" />
				<s:param name="inputcolspan" value="%{1}" />
			</s:datetimepicker>
			 <!-- Resolved Merging 4.4.2 and 4.5 Defect 34 start -->
			<td class="tabcenter" colspan="3" theme="bsimple">
			<!-- Resolved Merging 4.4.2 and 4.5 Defect 34 end -->	
							<s:param name="labelcolspan" value="%{4}" />
								<s:param name="inputcolspan" value="%{4}" />
							
					</td>
					
					<td class="tabcenter" colspan="1">
					<s:param name="labelcolspan" value="%{1}" />
								<s:param name="inputcolspan" value="%{4}" />
						<span id="availDateOfBirth" class="tabtextbold" />&nbsp; 
					</td>
			 <s:set name="gaurdianUserCheck" value="gaurdianUserCheck"/>
			   <s:if test="%{#gaurdianUserCheck=='gaurdianUserCheckless18'}">
			   <tr>
			<s:component cssClass="tabhead" template="/components/textcell.ftl"
				value="%{getText('subreg.label.idsection.garson')}">
				<s:param name="inputcolspan" value="%{4}" />
			</s:component>
			</tr>
			<s:hidden name="kinUserCheck" value="gaurdianUsernotCheck"/>
			
			<s:textfield name="kinFirstname" key="Subs.registration.label.garson.UserName" disabled="%{isDisable}"
				maxlength="15" required="!treeset.contains('kinFirstname')" />
			<s:textfield name="kinMiddlename" disabled="%{isDisable}" 
				key="Subs.registration.label.garson.MiddleName" maxlength="15" />
			<s:textfield name="kinLastname" key="systemparty.label.garson.lastName" disabled="%{isDisable}"
				maxlength="15" required="true" />
			
			<s:textfield name="kinRelationship" key="systemparty.label.garson.relationship" disabled="%{isDisable}"
				maxlength="15" required="!treeset.contains('kinRelationship')" />
				
			<s:select name="kinNationality" headerKey="" required="!treeset.contains('kinNationality')" disabled="%{isDisable}"
				headerValue="%{getText('select.label')}"
				key="channeluser.label.nationality"
				list="kinNationalTypeList" listKey="countryIso"
				listValue="description" /> 

			<s:textfield name="kinNationalityNo" key="subs.approval.label.kinNationalityNo" disabled="%{isDisable}"
				maxlength="%{checkExtCodeLen}" required="!treeset.contains('kinNationalityNo')" />
				
			<s:datetimepicker key="subs.approval.label.kinage"
				displayFormat="dd/MM/yyyy" value="%{'today'}" name="kinAge" required="!treeset.contains('kinAge')" id="datepicker">
				<s:param name="labelcolspan" value="%{1}" />
				<s:param name="inputcolspan" value="%{1}" />
			</s:datetimepicker>	
			
			<s:textfield name="sourceofIncome" key="channeluser.label.kinsourceof.income"  disabled="%{isDisable}"
				maxlength="20" required="!treeset.contains('sourceofIncome')" />
			
		 <s:textfield name="monthlyTurnOver" key="subs.approval.label.monthlyTurnOver" maxlength="20" disabled="%{isDisable}"
				 required="!treeset.contains('monthlyTurnOver')" />
		 <s:textfield name="kincontactNumber" key="subs.approval.label.kin.contact" maxlength="%{checkMsisdnLen}" disabled="%{isDisable}"
		 required="!treeset.contains('kincontactNumber')" />
	       <tr>
			<s:component cssClass="tabhead" template="/components/textcell.ftl"
				value=" ">
				<s:param name="inputcolspan" value="%{4}" />
			</s:component>
			</tr>
			
			</s:if>
			
			
           <!-- End By Dhananjay samal -->
           <tr>
			<s:select name="gender" key="subs.approval.label.gender" headerKey="" disabled="%{isDisable}"
				required="!treeset.contains('gender')" headerValue="Select" list="genderTypeList"
				listKey="enumId" listValue="description" />

			<%--<s:textfield name="gender" key="subs.approval.label.gender" maxlength="15" />
			--%>
			<s:select name="idType" headerKey="" required="!treeset.contains('idType')" disabled="%{isDisable}"
				headerValue="%{getText('select.label')}"
				key="subs.approval.label.idtype" list="_selectIdTypeList"
				listKey="enumCode" listValue="description" />

			<s:textfield name="idNo" key="subs.approval.label.idnumber" disabled="%{isDisable}"
				maxlength="40" required="!treeset.contains('idNo')" />

			<s:textfield name="idIssuePlace" disabled="%{isDisable}"
				key="Subs.registration.label.PlaceOfIssueOfId" maxlength="30"
				required="!treeset.contains('idIssuePlace')" />

			<s:select name="idIssueCountry" headerKey="" required="!treeset.contains('idIssueCountry')" 
				headerValue="%{getText('select.label')}" disabled="%{isDisable}"
				key="Subs.registration.label.IssueCountry"
				list="_idIssuecountryTypeList" listKey="countryIso"
				listValue="description" />

			<s:select name="residenceCountry" headerKey="" required="!treeset.contains('residenceCountry')"
				headerValue="%{getText('select.label')}" disabled="%{isDisable}"
				key="Subs.registration.label.ResidenceCountry"
				list="_residencecountryTypeList" listKey="countryIso"
				listValue="description" />
				</tr>
            <s:label name="explabel" id="explabel" value="Issue Date(dd/MM/yyyy)">
                <s:param name="labelcolspan" value="%{2}" />
				<s:param name="inputcolspan" value="%{2}" />
            </s:label>
			<s:datetimepicker  
				displayFormat="dd/MM/yyyy" value=""  name="idIssueDate" required="!treeset.contains('idIssueDate')">
				<s:param name="labelcolspan" value="%{2}" />
				<s:param name="inputcolspan" value="%{2}" />
			</s:datetimepicker>
              
            <s:label id="exp" name="exp" value="Expiry Date(dd/MM/yyyy)">
                <s:param name="labelcolspan" value="%{2}" />
				<s:param name="inputcolspan" value="%{2}" />
            </s:label>
			<s:datetimepicker  id="idExpiryDate"
				displayFormat="dd/MM/yyyy" value=""  name="idExpiryDate" required="!treeset.contains('idExpiryDate')">
				<s:param name="labelcolspan" value="%{2}" />
				<s:param name="inputcolspan" value="%{2}" />
			</s:datetimepicker>

			<s:checkbox name="isIdExpires" disabled="%{isDisable}" id="isIdExpires"
				key="Subs.registration.label.IsIDExpired" onclick="hidepicker()" value="true">
				<s:param name="labelcolspan" value="%{1}" />
				<s:param name="inputcolspan" value="%{1}" />
				<s:label name=""></s:label>
				<s:label name=""></s:label>
			</s:checkbox>


			<s:textfield name="address1" key="subs.approval.label.address1" disabled="%{isDisable}"
				maxlength="50" required="!treeset.contains('address1')" />
			<s:textfield name="district" key="subs.approval.label.address3" disabled="%{isDisable}"
				maxlength="50" required="!treeset.contains('district')" />
			<s:textfield name="city" key="subs.approval.label.city" disabled="%{isDisable}"
				maxlength="30" required="!treeset.contains('city')" />
			<s:textfield name="state" key="subs.approval.label.state" disabled="%{isDisable}"
		  required="!treeset.contains('state')"	maxlength="30" />
		  
		  <s:select name="country" headerKey="" required="!treeset.contains('country')" 
				headerValue="%{getText('select.label')}" disabled="%{isDisable}"
				key="Subs.registration.label.Country"
				list="_countryTypeList" listKey="countryIso"
				listValue="description" />
				
				<!-- Added By Dhananjay samal -->
				<!-- by gaurav
				<s:textfield name="birthPlace" key="channeluser.label.birthPlace"
				maxlength="30"  required="true"/>
				<s:select name="region" headerKey="" required="true"
				headerValue="%{getText('select.label')}"
				key="channeluser.label.region"
				list="regionList" listKey="grphDomainShortName"
				listValue="description" />
				--> 
				<!-- End By Dhananjay samal -->
				
			     <s:textfield name="postalCode" key="subs.approval.label.PostalCode"
				required="!treeset.contains('postalCode')" maxlength="20" />
                    
            
			<s:textfield name="employerName" disabled="%{isDisable}"
				key="subs.approval.label.EmployerName" maxlength="30"
				required="!treeset.contains('employerName')" />
			<!-- 
			<s:textfield name="retmsisdn" key="Subs.registration.label.retMsisdn"
				maxlength="%{checkMsisdnLen}" required="true" />
			<s:textfield name="distmsisdn"
				key="Subs.registration.label.distMsisdn"
				maxlength="%{checkMsisdnLen}" required="true" />
 -->
			<s:textfield name="remarks" key="subs.approval.label.remark" disabled="%{isDisable}"
				maxlength="100" />



			<!-- added for Mobinil merge 2.05 -->
			<!-- added for preferred language -->
			<!-- LANGUAGEDEFAULT removed header select to let languages come by default-->
			<s:select name="localeCode" headerKey="" required="true" disabled="%{isDisable}"
				 key="systemparty.label.language"
				list="localeList" listKey="languageCode" listValue="languageName">
				<s:param name="inputcolspan" value="%{1}" />
				<s:param name="labelcolspan" value="%{1}" />
			</s:select>
			<s:label name=""></s:label>
			<s:label name=""></s:label>
			<%--  merged for 2.0.0.12 merge  --%>
			<s:component cssClass="tabhead" template="/components/textcell.ftl"
				value="">
				<s:param name="inputcolspan" value="%{6}" />
			</s:component>
			<%-- ends here --%>

			<s:if test="companyAssociationAllowed">
				<s:component cssClass="tabhead" template="/components/textcell.ftl"
					value="%{getText('uti.association.information')}">
					<s:param name="inputcolspan" value="%{4}" />
				</s:component>
				<s:if test='isCompanyFormNoRequired.equals("Y")'>
					<s:label labelposition="center" key="utility.merchant.label.name">
						<s:param name="labelcolspan" value="%{1}" />
						<s:param name="inputcolspan" value="%{0}" />
					</s:label>

				</s:if>
				<s:else>
					<s:label labelposition="center" key="utility.merchant.label.name">
						<s:param name="labelcolspan" value="%{2}" />
						<s:param name="inputcolspan" value="%{0}" />
					</s:label>
				</s:else>

				<s:label key="subs.approval.label.accountNo" required="true">
					<s:param name="labelcolspan" value="%{2}" />
					<s:param name="inputcolspan" value="%{0}" />
				</s:label>
				<s:if test='isCompanyFormNoRequired.equals("Y")'>
					<s:label key="subs.approval.label.companyFormNo">
						<s:param name="labelcolspan" value="%{1}" />
						<s:param name="inputcolspan" value="%{0}" />
					</s:label>
				</s:if>

				<s:if test="slabsList.size > 0">
					<s:iterator id="row" value="slabsList" status="stat">
						<s:if test='isCompanyFormNoRequired.equals("Y")'>
							<s:select name="companyCode" list="billCompanyList" disabled="%{isDisable}"
								listKey="identifier" listValue="companyName" required="true"
								headerKey="" headerValue="Select">
								<s:param name="labelcolspan" value="%{0}" />
								<s:param name="inputcolspan" value="%{1}" />
							</s:select>
						</s:if>
						<s:else>
							<s:select name="companyCode" list="billCompanyList" disabled="%{isDisable}"
								listKey="identifier" listValue="companyName" required="true"
								headerKey="" headerValue="Select">
								<s:param name="labelcolspan" value="%{0}" />
								<s:param name="inputcolspan" value="%{2}" />
							</s:select>
						</s:else>
						<s:textfield name="accountNumber" maxlength="50" required="true" disabled="%{isDisable}">
							<s:param name="labelcolspan" value="%{0}" />
							<s:param name="inputcolspan" value="%{2}" />
						</s:textfield>

						<s:if test='isCompanyFormNoRequired.equals("Y")'>
							<s:textfield name="companyFormNo" maxlength="20" disabled="%{isDisable}">
								<s:param name="labelcolspan" value="%{0}" />
								<s:param name="inputcolspan" value="%{1}" />
							</s:textfield>
						</s:if>

					</s:iterator>
				</s:if>
			</s:if>
			<!-- 
			<s:if test="${popUpRequired =='Y'}">
				<tr>
					<td class="tabcol" colspan="4">
						<s:a href="javascript:assign()">
							<s:text name="%{getText('channeluser.link.appassociation')}" />
						</s:a>
					</td>

				</tr>
			</s:if>
			<s:if test="profileAssociationCounter > 0">


				<tr>
					<s:component cssClass="tabhead" template="/components/textcell.ftl"
						value="%{getText('channeluser.label.applicationName')}">
						<s:param name="inputcolspan" value="%{1}" />
					</s:component>
					<s:component cssClass="tabhead" template="/components/textcell.ftl"
						value="%{getText('channeluser.label.category')}">
						<s:param name="inputcolspan" value="%{1}" />
					</s:component>
					<s:component cssClass="tabhead" template="/components/textcell.ftl"
						value="%{getText('channeluser.label.gradeName')}">
						<s:param name="inputcolspan" value="%{1}" />
					</s:component>
					<s:component cssClass="tabhead" template="/components/textcell.ftl"
						value="%{getText('channeluser.label.profileName')}">
						<s:param name="inputcolspan" value="%{1}" />
					</s:component>
					<s:label name="applicationName">
						<s:param name="labelcolspan" value="%{1}" />
					</s:label>
					<s:label name="catName">
						<s:param name="labelcolspan" value="%{1}" />
					</s:label>
					<s:label name="gradeName">
						<s:param name="labelcolspan" value="%{1}" />
					</s:label>
					<s:label name="profileName">
						<s:param name="labelcolspan" value="%{1}" />
					</s:label>
				</tr>
				<s:label name="" key="">
					<s:param name="labelcolspan" value="%{1}" />
					<s:radio list="roleTypesMap" key="system.role.information"
						labelposition="center" value="${roleType}" name="roleType" />
				</s:label>
				<tr>
					<td class="tabcol" colspan="4">
						<s:a href="javascript:assignRole()">
							<s:text name="%{getText('channeluser.link.role')}" />
						</s:a>
					</td>
				</tr>
			</s:if>

			<s:if test="assignRoleList.size > 0">
				<s:if test="roleType==2">
					<s:label name="check" key="currently.groupRole.Selected">
						<s:param name="labelcolspan" value="%{2}" />
						<s:param name="inputcolspan" value="%{2}" />
					</s:label>
				</s:if>


				<s:if test="roleType==1">
					<s:label key="currently.system.Selected">
						<s:param name="labelcolspan" value="%{3}" />
					</s:label>
				</s:if>

				<s:set name="mCode" id="mCode" value="" />
				<s:set name="mCounter" id="mCounter" value="0" />
				<s:iterator value="assignRoleList" status="index">
					<s:if test="%{#mCounter==0}">
						<s:set name="mCode" value="%{moduleCode}" />
					</s:if>

					<s:if test="%{#mCode==moduleCode}">
						<s:if test="%{#mCounter==0}">
							<tr>
								<td class="tabcol" colspan="4">
									<strong><s:text name="%{getText(moduleCode)}" /> </strong>
								</td>
							</tr>
							<tr>
								<td class="tabcol" colspan="4">
									&nbsp;&nbsp;&nbsp;
									<s:text name="%{getText(roleName)}" />
								</td>
							</tr>
							<s:set name="mCounter" value="1" />
						</s:if>
						<s:else>
							<tr>
								<td class="tabcol" colspan="4">
									&nbsp;&nbsp;&nbsp;
									<s:text name="%{getText(roleName)}" />
								</td>
							</tr>
						</s:else>





					</s:if>
					<s:else>
						<tr>
							<td class="tabcol" colspan="4">
								<br>
								<strong> </strong>
								<br>
							</td>
						</tr>
						<tr>
							<td class="tabcol" colspan="4">
								&nbsp;&nbsp;&nbsp;
								<s:text name="%{getText(roleName)}" />
							</td>
						</tr>
					</s:else>

					<s:set name="mCode" value="%{moduleCode}" />

				</s:iterator>
			</s:if>
			 -->
			 <!-- by gaurav
			 -->
		    <s:if  test='(isConsumerPortelReq)'>			
			
			<s:if test='isAvailButtonRequiredForLogiId.equals("Y")'>
			<s:component cssClass="tabhead" template="/components/textcell.ftl"
				value="%{getText('systemparty.label.webinformation')}">
				<s:param name="inputcolspan" value="%{4}" />
			</s:component>
				<tr>
					<td class="tabtextbold">
						<s:text name="subscriber.label.webloginid" />
						<font color="red">*</font>:
					</td>
					<td class="tabcol">
						<s:textfield theme="simple" maxlength="%{maxLoginLength}" disabled="%{isDisable}"
							name="webLoginId" label="Msisdn" key="subscriber.label.webloginid" id="webLoginId" onkeydown="return checkSpace(event)"
							required="true" />
					</td>
					<td class="tabcenter" colspan="1" theme="bsimple">
						<s:submit key="button.check" cssClass="btn1" theme="bsimple"
							id="checkLoginIdAvail" onclick="checkLoginId(); return false;" />
					</td>
					<td class="tabcenter" colspan="1">
						<span id="availLoginId" class="tabtextbold" />&nbsp; 
					</td>
				</tr>
			
			</s:if>
			
			<s:else>
				<s:component cssClass="tabhead" template="/components/textcell.ftl"
				value="%{getText('systemparty.label.webinformation')}">
				<s:param name="inputcolspan" value="%{4}" />
				</s:component>
				<s:textfield name="webLoginId" required="true" disabled="%{isDisable}"
					maxlength="%{maxLoginLength}" key="subscriber.label.webloginid"
					onkeydown="return checkSpace(event)">
					<s:param name="labelcolspan" value="%{2}" />
					<s:param name="inputcolspan" value="%{2}" />
				</s:textfield> 
			</s:else>
				
			<!--random password generation from mobinil merge 2.05-->			
			<s:if  test='!(isRandomPassAllowed.equals("Y"))'>
				<s:password name="webPassword" key="subscriber.label.webpassword" disabled="%{isDisable}"
					maxlength="%{maxPasswdLength}" required="true" showPassword="true">
					<s:param name="labelcolspan" value="%{2}" />
					<s:param name="inputcolspan" value="%{2}" />
				</s:password>
				<s:password name="confWebPassword" disabled="%{isDisable}"
					key="subscriber.label.confirmpassword" maxlength="%{maxPasswdLength}" required="true"
					showPassword="true">
					<s:param name="labelcolspan" value="%{2}" />
					<s:param name="inputcolspan" value="%{2}" />
				</s:password>			
 		 
			</s:if> 
			 </s:if>
			
			
			 
			 
			<s:component cssClass="tabhead" template="/components/textcell.ftl"
				value="%{getText('subreg.label.idsection')}">
				<s:param name="inputcolspan" value="%{4}" />
			</s:component>
			<s:label value="%{getText('subsreg.label.type')}">
				<s:param name="inputcolspan" value="%{1}" />
			</s:label>
			<s:label value="%{getText('subsreg.label.docupload')}">
				<s:param name="inputcolspan" value="%{1}" />
			</s:label>
			<s:label value="%{getText('subsreg.label.typeofproof')}">
				<s:param name="inputcolspan" value="%{2}" />
			</s:label>
			<!-- Changes by Piyush 11/05/2012 start -->
			<s:if test="${proofType1Required =='Y'}">
				<s:file name="doc1" accept=" multipart/form-data" disabled="%{isDisable}"
					key="subsreg.label.proof1" value="" required="!treeset.contains('doc1')">
					<s:param name="inputcolspan" value="%{1}" />
					<s:param name="labelcolspan" value="%{1}" />
				</s:file>

			</s:if>
			<s:else>
				<s:file name="doc1" accept=" multipart/form-data" disabled="%{isDisable}"
					key="subsreg.label.proof1" value="">
					<s:param name="inputcolspan" value="%{1}" />
					<s:param name="labelcolspan" value="%{1}" />
				</s:file>

			</s:else>
			<s:select list="proofTypeList" headerKey="NA" headerValue="Select" disabled="%{isDisable}"
				listKey="enumCode" listValue="description" name="proofType1">
				<s:param name="inputcolspan" value="%{2}" />
			</s:select>

			<s:if test="${proofType2Required =='Y'}">
				<s:file name="doc2" accept="multipart/form-data" disabled="%{isDisable}"
					key="subsreg.label.proof2" value="" required="!treeset.contains('doc2')">
					<s:param name="inputcolspan" value="%{1}" />
					<s:param name="labelcolspan" value="%{1}" />
				</s:file>

			</s:if>

			<s:else>
				<s:file name="doc2" accept="multipart/form-data" disabled="%{isDisable}"
					key="subsreg.label.proof2" value="">
					<s:param name="inputcolspan" value="%{1}" />
					<s:param name="labelcolspan" value="%{1}" />
				</s:file>

			</s:else>

			<s:select list="proofTypeList" headerKey="NA" headerValue="Select" disabled="%{isDisable}"
				listKey="enumCode" listValue="description" name="proofType2">
				<s:param name="inputcolspan" value="%{2}" />
			</s:select>

			<s:if test="${proofType3Required =='Y'}">
				<s:file name="doc3" accept="multipart/form-data" disabled="%{isDisable}"
					key="subsreg.label.proof3" value="" required="!treeset.contains('doc3')">
					<s:param name="inputcolspan" value="%{1}" />
					<s:param name="labelcolspan" value="%{1}" />
				</s:file>

			</s:if>

			<s:else>
				<s:file name="doc3" accept="multipart/form-data" disabled="%{isDisable}"
					key="subsreg.label.proof3" value="">
					<s:param name="inputcolspan" value="%{1}" />
					<s:param name="labelcolspan" value="%{1}" />
				</s:file>

			</s:else>
			<!-- Changes by Piyush 11/05/2012 end -->
			<s:select list="proofTypeList" headerKey="NA" headerValue="Select" disabled="%{isDisable}"
				listKey="enumCode" listValue="description" name="proofType3">
				<s:param name="inputcolspan" value="%{2}" />
			</s:select>

			<!-- 
			<tr>
				<td class="tabcenter" colspan="6">
					<s:submit key="button.submit" theme="bsimple" cssClass="btn1" />
				</td>
			</tr>
			 -->
			 <tr>
			 <td class="tabcenter" colspan="4" />
			 <s:if test="mandatoryList.size > 0">
          <s:iterator value="mandatoryList" status="stat" >
          <s:set name="flag" value="#stat.index" />
          <s:set name= "type" value="mandatoryList[${flag}].fieldType" />
          <s:set name= "name" value="mandatoryList[${flag}].fieldName" />
          <s:set name= "length" value="mandatoryList[${flag}].maxLength" />
          <s:set name= "list" value="mandatoryList[${flag}].selectionList" />
          <s:set name= "key" value="mandatoryList[${flag}].listKey" />

         <s:if test="%{'${type}'=='textfield'}">
         <s:textfield name="${name}" key="label.${name}"  disabled="%{isDisable}"
          maxlength="${length}" required="true" />			
		   </s:if>
         <s:if test="%{'${type}'=='selection'}">
         <s:select name="${name}" key="label.${name}"  disabled="%{isDisable}"
          required="true" 
          list="list" listKey="${key}"
          listValue="description" />
         </s:if>
       
         </s:iterator>
          <s:label name=""></s:label>
		<s:label name=""></s:label>	
         </s:if>
         
        </td>
        </tr>
        
        
        <tr>
			 <td class="tabcenter" colspan="4" />
			 <s:if test="optionalList.size > 0">
          <s:iterator value="optionalList" status="stat" >
          <s:set name="flag1" value="#stat.index" />
          <s:set name= "type1" value="optionalList[${flag1}].fieldType" />
          <s:set name= "name1" value="optionalList[${flag1}].fieldName" />
          <s:set name= "length1" value="optionalList[${flag1}].maxLength" />
          <s:set name= "list1" value="optionalList[${flag1}].selectionList" />
          <s:set name= "key1" value="optionalList[${flag1}].listKey" />

         <s:if test="%{'${type1}'=='textfield'}">
         <s:textfield name="${name1}" key="label.${name1}"  disabled="%{isDisable}"
          maxlength="${length1}"  />			
		   </s:if>
         <s:if test="%{'${type1}'=='selection'}">
         <s:select name="${name1}" key="label.${name1}"  disabled="%{isDisable}"
          list="list1" listKey="${key1}"
          listValue="description" />
         </s:if>
         </s:iterator>
         <!-- Resolved Merging 4.4.2 and 4.5 Defect 38 start -->
          <%-- <s:label name=""></s:label>
		<s:label name=""></s:label>	 --%> 
         </s:if>
        </td>
        </tr>
        <!-- end -->
			 <!-- <tr>
				<td class="tabcenter" colspan="4" /> -->
		<!-- Resolved Merging 4.4.2 and 4.5 Defect 38 end -->
			<tr>
				<td class="tabcenter" colspan="4">
					<s:submit key="button.next" theme="bsimple" cssClass="btn1" disabled="%{isDisable}"
						action="subsRegistrationServiceBean_output" />
					<s:reset key="button.reset" theme="bsimple" cssClass="btn1" disabled="%{isDisable}" />
				</td>
			</tr>
		</s:form>

		<%
			if (request.getAttribute("accountNumber") != null) {
				List lstAccounts = (List) request.getAttribute("accountNumber");
				for (int i = 0; i < lstAccounts.size(); i++) {
					out
							.println("<script>document.subsRegistrationServiceBean.accountNumber["
									+ i
									+ "].value='"
									+ lstAccounts.get(i)
									+ "';</script>");
				}
			}
			if (request.getAttribute("companyCode") != null) {
				List lstAccounts = (List) request.getAttribute("companyCode");
				for (int i = 0; i < lstAccounts.size(); i++) {
					out
							.println("<script>document.subsRegistrationServiceBean.companyCode["
									+ i
									+ "].value='"
									+ lstAccounts.get(i)
									+ "';</script>");
				}
			}
			if (request.getAttribute("companyFormNo") != null) {
				List lstAccounts = (List) request.getAttribute("companyFormNo");
				for (int i = 0; i < lstAccounts.size(); i++) {
					out
							.println("<script>document.subsRegistrationServiceBean.companyFormNo["
									+ i
									+ "].value='"
									+ lstAccounts.get(i)
									+ "';</script>");
				}
			}
		%>

		<%--Added By piyush for CR - Add Check Button for Customer MSISDN and External Code during Registration	--%>
		<script src="<%=request.getContextPath()%>/js/TangoAjax.js"></script>
		<script src="<%=request.getContextPath()%>/mjsp/dep-lib/json.js"></script>
		<script type="text/javascript">
		  var appContext = "<%=request.getContextPath()%>";
     	  function checkMsisdn(){  
       		getMsisdn = document.getElementById("msisdn").value;
			if(getMsisdn==null||getMsisdn==""){
					alert("Enter MSISDN first");	
			}		
			else{
			getMsisdn = getMsisdn.replace('&','|');
			getMsisdn = getMsisdn.replace('%','|');
			var url = "/party/subsRegistrationServiceBean_checkMsisdn.action?getMsisdn="+getMsisdn;
			var result = processAjaxRequest(url);  
			document.getElementById("availMSISDN").innerHTML=result;}
			return false;
  		}
       	  
       	
  		
      	  function checkLoginId(){  
      		  getLoginId = document.getElementById("webLoginId").value;
      		 <%-- DEF1289 start --%>
      		 if(getLoginId.indexOf(">") > -1||getLoginId.indexOf("<") > -1){
      			document.getElementById('subsRegistrationServiceBean').action  = "login_logedout.action";
      			document.getElementById('subsRegistrationServiceBean').submit();
      		}else{
      		<%-- DEF1289 end --%>
  			if(getLoginId==null||getLoginId==""){					
  					alert('<s:text name="subscriber.loginid.empty"/>');
  			}
  			else{
  				getLoginId = getLoginId.replace('&','|');
  				getLoginId = getLoginId.replace('%','|');
  			var url = "/party/subsRegistrationServiceBean_checkLoginId.action?getLoginId="+getLoginId;
  			var result = processAjaxRequest(url);  
  			document.getElementById("availLoginId").innerHTML=result;
			}
			return false;
		}
		}
		
	function	checkDateOfBirth(){
	  //var getInputDob1 =document.getElementById("msisdn").value;
	  //var getInputDob=document.getElementById("inputDob1").value;
	  
	  //var picker = dojo.widget.byId("inputDob1");
     
     //string value
     var stringValue = picker.getDate();
	  
	    
		alert(stringValue);
			if(getInputDob==null||getInputDob==""){
					alert("Enter Date Of Birth ");	
		    	}		
			else{
			getInputDob = getInputDob.replace('&','|');
			getInputDob = getInputDob.replace('%','|');
			var url = "/party/subsRegistrationServiceBean_checkDateOfBirth.action?getInputDob="+getInputDob;
			var result = processAjaxRequest(url);  
			document.getElementById("availDateOfBirth").innerHTML=result;
			}
			return false;
		
		}
	
		function checkExtCode(){ 
			getExtCode = document.getElementById("externalCode").value;
			if(getExtCode==null||getExtCode==""){
					alert("Enter Identification Number first");	
			}		
			else{ 
			getExtCode = getExtCode.replace('&','|');
			getExtCode = getExtCode.replace('%','|');
			var url = "/party/subsRegistrationServiceBean_checkExtCode.action?getExtCode="+getExtCode;
			var result = processAjaxRequest(url);  
			document.getElementById("availExtCode").innerHTML=result;
			return false;
			}
		}
		function processAjaxRequest(url){  
			return getAjaxResult(url);
		}	
		function getAjaxResult(url){
			
		      var request = getNewXMLHttpRequest();
		    
		      url = appContext +url;
		      request.open('GET',url,false);
		      var responseMessage = request.send(null);
		      var ajaxData = request.responseText;
			  return ajaxData;
		}
		//Start Added for Aadhaar Card Integration
		
		
		var apiCallStatus = false;
		var appletResponse = 0;
		
		function getEKycForUID() {
			alert("Function Invoked");
			var getUanumber=document.getElementById('eKycUID').value;

			
			var getUanumber=document.getElementById('eKycUID').value;
	   		var getAuth_xml = document.getElementById("auth_xml").value;
	   		var getIsSigned = document.getElementById("isSigned").value;
	   		var getAadharNumber = getUanumber;
	   		var aadharUidLen=document.getElementById('aadharUidLen').value; 
	   		alert("Function Invoked");
	   		      
	    	var aadhaarRegularExpression = /^[0-9]+$/;     
	    	if (getUanumber == null || getUanumber == ""){       
	        	alert("Please enter aadhar number.");       
	        	return false; 
	    	} else if(getUanumber.length != aadharUidLen){       
	       		alert("Aadhaar number can only be 12 digits long.");       
	       		return false;
	   		} else if(!aadhaarRegularExpression.test(getUanumber)){
	       		alert("Aadhaar number can be digits only.");
	       		return false;
	   		}
	   		
	   		alert("Validation is sucessfull. Please keep the finger on device and authenticate.");
	   		
	   		appletResponse = 0;

			var valueMap={}; // creating a value map for json    
	    	valueMap["uanumber"] = getUanumber; 
	     	apiCallStatus = false;
	    	
	    	
	    	var jsonstr = JSON.stringify(valueMap, null, 10);
	    	
	    	
	        
	      	document.uidfrm.captureFPWithSignatureForEKYC(jsonstr);
	      	   
	      	alert("Back from Applet " + apiCallStatus);
	      	   		
	        if (appletResponse != 0) {
	      //  	alert("Returning from Java Script");
	        	return false;
	        }
	      
	      	getAuth_xml = document.getElementById("auth_xml").value;
	      	
	      	alert("Aadhaar Code is " + getAadharNumber + " Response Received From  Applet "+ appletResponse + " IsSigned = "+ getIsSigned);
	   		//getAuth_xml = getAuth_xml.replaceall("+", " ");
	   		alert("temp_auth_xml "+getAuth_xml);
	      	      
	    	var url = "/party/subsRegistrationServiceBean_checkEKYCAadharUID.action?isSigned="+getIsSigned+"&aadharNumber="+getAadharNumber+"&auth_xml="+getAuth_xml;
	    	
	    	var result = processAjaxRequest(url);
			
			alert('Result '+result);
			
			var resultArray = result.split("|");  
			if (resultArray[0]== "Y") {
				$("input,select").removeAttr("disabled");
				document.getElementById("checkUIDKycAvail").disabled = true;
				document.getElementById("eKycUID").disabled = true;
			} else {
				 $("input,select").removeAttr("disabled");
			}
			document.getElementById("availUidKycAadhar").innerHTML=resultArray[1];
			alert(resultArray[2]);
			return false;
			}	

			
		function validateBiometricInformation(){  
			    
	   
	     	var getUanumber=document.getElementById('uID').value;
	   		var getAuth_xml = document.getElementById("auth_xml").value;
	   		var getIsSigned = document.getElementById("isSigned").value;
	   		var getAadharNumber = getUanumber;
	   		var aadharUidLen=document.getElementById('aadharUidLen').value; 
	      
	    	var aadhaarRegularExpression = /^[0-9]+$/;     
	    	if (getUanumber == null || getUanumber == ""){       
	        	alert("Please enter aadhar number.");  
	        	return false; 
	    	} else if(getUanumber.length != aadharUidLen){       
	       		alert("Aadhaar number can only be 12 digits long.");       
	       		return false;
	   		} else if(!aadhaarRegularExpression.test(getUanumber)){
	       		alert("Aadhaar number can be digits only.");
	       		return false;
	   		}
	 
	 
	   		alert("Validation is sucessfull. Please keep the finger on device and authenticate.");
	        
	        document.uidfrm.checkDeviceConnected();
	        alert("Fingerprint Captured successfully");
	        if (appletResponse != 0) {
	        //	alert(" -------- Device Not Connected/Detected -------");
	        	$("input,select").removeAttr("disabled");
	        	document.getElementById('uID').disabled=true;	
	        	document.getElementById('checkUIDAvail').disabled=true;	
	        	return false;
	        }
	        
	        appletResponse = 0;
	        
			var valueMap={}; // creating a value map for json    
	    	valueMap["uanumber"] = getUanumber; 
	     	apiCallStatus = false;
	    	
	    	
	    	var jsonstr = JSON.stringify(valueMap, null, 10);
	    	
	    	
	        
	      	document.uidfrm.captureAndRetrievePayloadWithFPWithSignature(jsonstr);  
	      	//document.uidfrm.captureFPWithSignatureForEKYC(jsonstr);
	        
	     //   alert("Back from Applet " + apiCallStatus);
	        if (appletResponse != 0) {
	      //  	alert("Returning from Java Script");
	        	return false;
	        }
	        
	      	getAuth_xml = document.getElementById("auth_xml").value;
	      	getIsSigned = document.getElementById("isSigned").value;
	   		getAadharNumber = document.getElementById("uID").value;
	   		   		
	   		//alert("Aadhaar Code is " + getAadharNumber + " Response Received From  Applet "+ appletResponse + " IsSigned = "+ getIsSigned);
	   		//alert("temp_auth_xml "+getAuth_xml);
	/*
	      	$("input,select").removeAttr("disabled");
	        
	        if(appletResponse == 0) {
	                	$("input,select").removeAttr("disabled");
	        }  
	  */
	  //  	alert("TEsting");
	    	var url = "/party/subsRegistrationServiceBean_checkAadharUID.action?isSigned="+getIsSigned+"&aadharNumber="+getAadharNumber+"&auth_xml="+getAuth_xml;
	    	//var url = "/party/subsRegistrationServiceBean_checkAadharUID.action?isSigned="+getIsSigned+"&aadharNumber="+getAadharNumber+"&auth_xml=abcd";
	  //  	alert("Call "+url);
			var result = processAjaxRequest(url);
			
			var resultArray = result.split("|");  
			if (resultArray[0]== "Y") {
				$("input,select").removeAttr("disabled");
				document.getElementById("checkUIDAvail").disabled = true;
				document.getElementById("uID").disabled = true;
			} else {
				 $("input,select").removeAttr("disabled");
			}
			document.getElementById("availUidAadhar").innerHTML=resultArray[1];
	    
	   // 	 alert("Returing ");
	        return false; 
	        
	   }
			
			
		function onFailurePayloadGeneration(errorCode, errorMessage) {   
			alert(errorMessage);
			appletResponse = errorCode;
			//alert("Error Code " + appletResponse + "Error "+ errorCode);
	    	apiCallStatus = false;
		}

		function onSuccessPayloadGeneration(sucessMessage,status) { 
			var auth_length;
			alert(sucessMessage );
			auth_length = sucessMessage.length;
			alert(auth_length);
			appletResponse = 0;
			document.getElementById("auth_xml").setAttribute("value", sucessMessage);
	    	apiCallStatus = true;
	    }

		function onAuthenticationStatus(statusCode, statusMessage,status) {
	    	if(eval(status)){
	        	alert('!!!!!!!!!!!!!YES SUCCESSFUL!!!!!!!!');
	    	} else {
	        	alert(statusMessage+"\n"+statusCode);
	    	}
	    }
			
			
		//End Added for Aadhaar Card Integration
	</script>
	
		<script src="<%=request.getContextPath()%>/js/TangoAjax.js"></script>
	</body>

</html>
