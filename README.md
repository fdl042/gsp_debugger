# gsp_debugger

How to check backend variable value from browser console

Created by Dongmin Liu

The front end development needs to access the backend variables value from the gsp page. But, there is no tools ready to use for this purpose.  This document is to show you how to know all the variables available on the page.

Step-by-step guide
To leverage the template I wrote at /grails-app/views/common/includes/utility/_debugger.gsp, 

%{--   debug helper to show gsp variables in Javascript objects window.data --}%


    <g:javascript>
      window.data = window.data || {};
      <g:each in="${pageScope.getVariableNames()}" >
        <g:if test="${it != 'session' && (! it.contains('.')) }">
          window.data.${it} = '${pageScope.getVariable(it)}';
        </g:if>
      </g:each>
    </g:javascript>




you need include_debugger.gsp in your _footer.gsp file. For example,

views/common/includes/_footer.gsp adds the following line:
<g:render template="/common/includes/utility/debugger" />

You can control this debugger disabled/enable by grails feature toggle. This toggle should be enabled on Dev and Integration env by default. It should be disabled by default for other environment. 

Load your page from the browser. You don't have to restart the grails app for this change. 

In browser console: type window.data you should be able to see all the available variables


