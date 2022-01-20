# example-java-tanpa-db



private void procDeactiveDocumentSavePusat(RoutingContext context) {
		final JsonObject principalUser = context.user().principal();

		responseBody = new JsonObject();
		final JsonObject requestBody =new JsonObject(context.getBodyAsString());
		final JsonObject jsonReqColumn =requestBody.getJsonObject(Dukcapil.KEY_REQ_TABLE);

		final JsonArray paramIn = new JsonArray();
		paramIn.add(jsonReqColumn.getString("SID"));
		paramIn.add(Long.parseLong(principalUser.getString("username")));
		paramIn.add(jsonReqColumn.getString("ALASAN"));

		final JsonArray paramOut = new JsonArray();
		paramOut.addNull();
		paramOut.addNull();
		paramOut.addNull();
		paramOut.add(java.sql.Types.SMALLINT);
		paramOut.add(java.sql.Types.VARCHAR);
		paramOut.add(java.sql.Types.VARCHAR);
		
		responseBody.put(Dukcapil.RESP_MESSAGE,'berhasil disimpan';
		responseClientSuccess(context, responseBody);
/*
		dbService.callQuery(this.PROC_DEACTIVE_SAVE_PUSAT, paramIn, paramOut, res -> {
			if (res.succeeded()) {
				JsonArray resultDb = res.result();
				int status =resultDb.getInteger(3);
				if (status != Dukcapil.RESP200) {
					responseBody.put(Dukcapil.RESP_MESSAGE, resultDb.getString(4));
					responseClientError(context, status, responseBody);
				} else {
					responseBody.put(Dukcapil.RESP_MESSAGE, resultDb.getString(4));
					JsonObject respData =new JsonObject(resultDb.getString(5));
					
					JsonObject jsonBsre = new JsonObject();
					jsonBsre.put("SEQN_ID", respData.getString("SEQN_ID"));
					jsonBsre.put("CERT_STATUS", 7);
					
					JsonObject jsonKafkaBsre=new JsonObject();
					jsonKafkaBsre.put(DukcapilKafka.KEY_HEADERS,new JsonObject().put("ACTION", "UPDATE"));
					jsonKafkaBsre.put(DukcapilKafka.KEY_DATA,jsonBsre);
					
					activityDesc =new StringBuilder();
					activityDesc.append("NO. SURAT/AKTA : ");
					activityDesc.append(respData.getString("ANAK_NO"));
					activityDesc.append("<br/>NIK : ");
					activityDesc.append(respData.getString("ANAK_NIK"));
					activityDesc.append("<br/>NAMA LENGKAP : ");
					activityDesc.append(respData.getString("ANAK_NAMA_LGKP"));
					
					JsonObject mapActifity =new JsonObject();
					mapActifity.put(DukcapilActivity.ACTIVITY_DATE, dukcapilLibs.getStringToday01());
					mapActifity.put(DukcapilActivity.ACTIVITY_TYPE, DukcapilActivity.ACTION_AC00);
					mapActifity.put(DukcapilActivity.ACTIVITY_MOD, DukcapilActivity.MODULE_CPL_PGKN);
					mapActifity.put(DukcapilActivity.ACTIVITY_NO_DOC, respData.getString("ANAK_NO"));
					mapActifity.put(DukcapilActivity.ACTIVITY_DESC, activityDesc.toString());
					mapActifity.put(DukcapilActivity.ACTIVITY_IP_ADDRESS, principalUser.getString("ip_address"));
					mapActifity.put(DukcapilActivity.ACTIVITY_IP_PROXY, principalUser.getString("ip_proxy"));
					mapActifity.put(DukcapilActivity.ACTIVITY_VER_CLIENT, principalUser.getInteger("versi_client"));
					mapActifity.put(DukcapilActivity.ACTIVITY_VER_PROXY, principalUser.getInteger("versi_proxy"));
					mapActifity.put(DukcapilActivity.ACTIVITY_USER_ID, principalUser.getString("username"));
					mapActifity.put(DukcapilActivity.ACTIVITY_NO_PROP, respData.getInteger("NO_PROV"));
					mapActifity.put(DukcapilActivity.ACTIVITY_NO_KAB, respData.getInteger("NO_KAB"));		
					
					jsonKafkaBsre.put(DukcapilKafka.KEY_DATA_ACTIVITY,mapActifity);
					toKafkaBsreCapil(DukcapilKafka.TOPIC_BSRE_AKUI_ANAK, "0000",jsonKafkaBsre);
					
					JsonObject jsonMaster = new JsonObject();
					jsonMaster.put("ANAK_NO", respData.getString("ANAK_NO"));
					jsonMaster.put("CERT_STATUS", 0);
					
					JsonObject jsonKafkaMaster=new JsonObject();
					jsonKafkaMaster.put(DukcapilKafka.KEY_HEADERS,new JsonObject().put("ACTION", "UPDATE"));
					jsonKafkaMaster.put(DukcapilKafka.KEY_DATA,jsonMaster);
					toKafkaCapil(DukcapilKafka.TOPIC_CAPIL_AKUI_ANAK, "0000",jsonKafkaMaster);
					
					responseClientSuccess(context, responseBody);
				}
			} else {
				responseBody.put(Dukcapil.RESP_MESSAGE, res.cause().getMessage());
				responseClientError(context, responseBody);
			}
		});
	*/
	}
