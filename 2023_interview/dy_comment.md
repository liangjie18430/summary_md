# xigua
"基于头条数据训练的模型，点赞\回复作为目标，特征包括点赞数\率、回复数\率等统计特征，文本模型分，评论作者近期评论特征等
property_category_1 in VEC('video_news','video_vlog','video_agriculture', 'video_food', 'video_music', 'video_others'"




# dy comment

"粗排，top100进精排
(1+1882.080977*(digg_wilson+5.930004*reply_wilson))^1*(1+0.379712*log(digg_cnt+1))^2.205032*(1+0.381645*log(reply_cnt+1))^0.381645"

"依照精排得分及融合公式重新进行排序，top评论进热门，其余评论按时间序排列
不上热门：大表情，全局重复度高，视频下重复评论，相关度得分<0.43
热点：
    6条热门
其他：
    15条热门；
时间序前20条以消费质量分模型和时间加权倒序"
